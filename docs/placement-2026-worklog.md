# Placement Worklog — 2026 (Parts 1–3)

> Dictated by Jack, 2026-08-09. Resume point: end of MIS load-test write+read benchmarking.
> Target format: **CV experience bullet points** (LemonPhase/jack-cv update; confirmed by Jack).

## Placement basics
- 6-month industrial placement, **part of MEng degree**, full-time
- **30 Mar 2026 → 18 Sep 2026** (ongoing as of Aug 2026)
- Employer: **"US-based hedge fund"** for now — update name after placement ends (Sep 2026)

## System overview — news ingestion
- Ingest news articles from various sources → store → normalise → optional **LLM screening** (labelling + summaries) → frontend for traders/researchers
- **Pipelines** (Dagster): web scraping / API calls (fully compliant) → raw articles to **S3** → normalise to markdown → normalised bucket → register in **MIS**
- **MIS** (Metadata Indexing Service): Python FastAPI + Postgres, indexes all ingested documents. Some sources have a trigger that runs screening (summaries, topics, categories) writing to MIS metadata
- **Workbench** (frontend): xh.hoist (React + Groovy, internal version — team mandate). Groovy was legacy backend; team built **"api"** (Python FastAPI) as the real backend — Groovy now just proxies to it (still handles auth). When Jack joined (April) api was freshly initialised, mostly a proxy to MIS; many features added since

## Work in time order

### 1. Mock pipeline (first task)
- Purpose: test end-to-end wiring before real news feeds available
- Generates predefined random articles, runs same flow as real pipelines:
  ingest (random generation) → normalise (to markdown) → collect (store raw + normalised, write metadata to MIS)
- Hands-on intro to the whole pipeline

### 2. Main project: load-test & benchmark MIS
- Motivation: heavy ingest load (Bloomberg trial peaked ~200k docs/day) + concurrent bulk reads
- Open-ended → decomposed: **write then read**, local first then hosted (hosted not done)
- **Tooling**: Locust (easy setup, comprehensive config + monitoring)
- **Harness**: request shapes mirrored from frontend & api; varied news pipeline shapes for write; pgdump of dev DB into local Postgres (Docker)
- Line manager suspected **Postgres** as the bottleneck — checked in with him throughout

#### Write test — bottlenecks found, in order
1. **Connection pool**: default ~10/20 → raised to 40, 80 → diminishing returns, no longer bottleneck
2. **Uvicorn workers**: 4 → 16, near-linear RPS gain
3. **Locust process**: single Python event loop → C implementation + parallel runs → saturated local CPU
- Workload: **1:2 create:update** (line manager's estimate); updates on only ~100 articles → **row-lock contention** visible in Postgres monitoring (time waiting on locks)
- Result on local 16-core / 64 GB: **~1000 RPS write, p95 577 ms**

#### Read test
- Goal: high-leverage indexes that don't hurt write (write had headroom)
- Round 1: tested each index against target queries → composite indexes gave **+10–16% RPS, −10–12% p50 latency**
- MIS query changes happened → Round 2:
  - `created_at` index: REST endpoint read **+129.9% RPS**
  - composite (data source + date): GraphQL queries **+33.6% RPS**
  - Together: **+126.2%** and **+36.1%**
- Time-in-read analysis (small vs large corpus):
  - Small queries: 47% COUNT query (before each read) / 51% main db execution
  - Large corpus: 31% COUNT / 69% db_execution
  - Ruled out pydantic serialisation & ORM hydration — it's DB-bound → indexes were the fix; **deployed later**

### 3. API service work
- Most "features" = wiring, maintenance, field corrections — not CV-worthy per Jack
- **Auth layer (CV-worthy)**: API previously accessible by ANY machine that could reach the cluster in the VPC. Added authentication: bearer token passed from frontend (Jack also wired the frontend passing) → authenticates user to **Microsoft Entra ID**. Critical endpoints gated. Per-resource authorisation not yet implemented (not required now) — will build on Jack's auth endpoint.
  - VPC/cluster detail (resolved 2026-08-13): it's a plain **Kubernetes cluster**; inter-service comms go **out through the edge and back in via the GLOBAL URL** — not in-cluster internal `svc.<ns>` DNS. So the API sits behind the edge at a global URL; exposure = any client that could reach the edge/VPC. CV phrasing leans to "added auth to a service exposed via the cluster edge, previously callable by any machine that could reach it" — a genuine security closure

### 4. Chat agent (flagship project — highest CV leverage)
- Idea with line manager; **prototyped in 3 days**; natural-language interface to existing data infra (pipeline + MIS) for end users
- Domain context: **feeds mainly commodities**; frontend "all documents" tab = **commodities scanner**; **Bloomberg was a paid trial, stopped** (expensive, few users) — the 200k docs/day figure came from the trial
- Prototype (3 days): whoosh (in-memory search in api) + NL search endpoint returning MIS docs; **litellm** backend; assistant UI tab in workbench
- Senior manager liked it → production push:
  - Search: whoosh → **deployed Manticore**; syncs with MIS (documents uploaded to Manticore index on ingest)
  - Backend: → **langchain deepagents** (context mgmt + thread mgmt; checkpointing stores chat threads; pairs with litellm proxy)
  - Frontend: experimented **OpenUI** (generated UI); shown to senior manager, liked
- **MCP server**: Jack spun up + deployed; ~proxy to api endpoints; goal: generalise search so users can connect their own Claude/GPT, not just workbench
- Weird structure (acknowledged): search endpoint on api → Manticore; chat stream endpoint on api; MCP standalone but calls search on api (could internalise later)
- **Ownership**: Jack single-handedly: all frontend + backend agent (deepagents) + MCP; line manager: search index (Jack tuned a few fields for better results)
- **Usage / impact (answered 2026-08-12)**: early prototype stage; **~20 people in the pilot group**; **~20 queries/day** at time of writing (may increase); corpus **~130k documents indexed**. One PM described it as a **"game changer"** — good for CV impact phrasing
- Jack's explicit contributions:
  - Source URL rendering
  - Web search + Exa search integration
  - Fixed agent-stopping bug: deepagents auto-compaction (summarisation middleware) streamed its output like normal output through the ungated endpoint → OpenUI parser choked on pure markdown → added a gate so compaction output stays in backend

### 5. Agent evals + optimisation (ongoing) — flagship differentiator
- **LangSmith tracing**: enabled via config; every deepagent call traced → observability is the foundation of eval (see which component caused good/bad results; like logging for debugging)
- Context: another dev at the firm evals a different agent — theirs more deterministic (output programmatically checkable); ours is a **research agent**, less quantitative
- **Evals harness (designed + implemented by Jack, still ongoing)** — based on a LangChain blog on agent evals:
  - Trigger: real user feedback — searched topic + specific date, only 3/4 expected articles appeared → **recall** is the key metric
  - Framework: LangSmith experiments/datasets; general run-and-evaluate framework; each experiment = JSON examples of (input query, output evaluator), evaluator varies by experiment type
  - **Recall eval**: expected doc IDs; evaluator checks they appear in the agent answer's source list
  - **Recency eval**: does the agent know current date + use it? Queries like "weekly update on [topic]"; evaluator checks searched/used docs are within a week of today
- **Date range input**: added to search input + MCP — text matching on dates isn't deterministic → Manticore native date-range filtering supplied by the LLM (optional)
- **Context-window optimisation** (with evals as safety net):
  - Problem: search tool results almost always too large; deepagents toolcall middleware offloads to internal filesystem + terminal navigation
  - Fix: trimmed document metadata in search results (they included LLM screening labels); kept only important metadata + summary + topics → agent gets high-level content without blowing context
  - Result: **−90% tokens per search query, −70% total tokens per recall query, 0% recall impact**
- **MCP tools** (3): `index` (search-index stats, doc count), `search` (Manticore text search, BM25, ranked metadata + limit + date filters), `get_document` (raw + normalised content by doc ID) → agent inspects content it deems relevant
- Future fine-grain (acknowledged, deferred): analyse search terms used vs MCP returns per term; currently call-traced + end-to-end eval is sufficient

---

## Infrastructure ownership & environment (answered 2026-08-12)
- **K8s cluster**: managed by **devops** (not Jack) — but Jack did hands-on ops work: wrote/used **Helm charts**, viewed pod status via **Headlamp** (K8s UI) + **kubectl**, used **Datadog** for metrics and logs to debug issues
- **RDS (Postgres)**: managed by **database admin team** — not Jack's infra
- **CV takeaway**: infrastructure itself is shared/team-managed; Jack's ownership is at the **application layer** (services, agent, MCP, evals) + hands-on debugging on the cluster. Phrase as "debugged production issues on K8s (Helm, Headlamp, kubectl, Datadog)" rather than "managed the cluster"

---

### 6. Founding engineer — 15 AI (startup) (dictated 2026-08-13) — NEW CV material
- **15 AI** — a DIFFERENT venture from KEATH.AI
- Role: **founding engineer**; dates: **Mar 2025 – Apr 2026** (quit because it conflicted with the placement; note it overlaps Goodnotes Jun–Sep 2025 and the first month of placement — likely part-time during term, flag for CV honesty)
- **Nothing launched** — rapidly building prototypes; **CEO pivoting frequently** (Jack found this annoying)
- Project 1 — **KOL search engine**: scrapes Key Opinion Leaders; search engine for KOL contacts, queryable by products / tags
- Project 2 — **blog website**: built with **Astro**
- Jack's read: not high leverage. Assistant's call (2026-08-13): **include, but compact** — founding engineer × 13 months is real founder signal + fills the timeline; frame around what was built + ownership, NOT the pivoting/CEO frustration; 1–2 bullets max, never lead with it

---

*Open source / GitHub links (2026-08-13): Jack confirms GitHub link is weak — no OSS contributions, no completed OSS repos; all work has been inside organisations. Deprioritised on the CV unless decided otherwise. (Counterpoint discussed: the PROBE repo itself is a real public research artifact — a link may still carry weight for AI/ML roles even while in progress.)*

*Next: no further placement chunk — evals (§5) is the current/last workstream (confirmed 2026-08-13). Outstanding CV decisions: Year 3 items (PROBE/Computing Research Collective, robotics 2nd place — Jack unsure), GitHub links (deprioritised), 1 vs 2 pages. Placement + startup material now complete — ready to draft CV experience section (awaiting Jack's go-ahead).*
