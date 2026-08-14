# CV Update Plan — ranked by market leverage

**Source evidence:** `docs/job-market-analysis-2026.md` (76 real JDs, 2026-08-13)
**Ranking logic:** gap size (what's missing) × demand frequency (JD %) × rarity (what few candidates have).

---

## P0 — MUST DO (biggest gaps × highest demand)

### 1. Add the hedge fund role — the flagship entry (currently 100% missing from CV)
This is the single most important change. It directly hits the top AI-engineer JD requirements: LLM stack (73%), agents (53%), evals (53%), production/deployment (67%).

**Framing — 1 role entry, 4 bullets, "ownership from idea to production" language:**

> **US-based Hedge Fund** · Software Engineer — Mar 2026 – present
> - Built a production LLM chat agent over a **130k-document news corpus** (langchain deepagents, Manticore search, OpenUI), prototyped in 3 days and deployed to a **~20-user pilot**; described by a PM as a **"game changer"**
> - Designed and implemented the **LangSmith evaluation harness** (recall + recency evals, driven by real user feedback); trimmed search-result metadata → **−90% tokens/search, −70% total tokens/query, 0% recall impact**
> - **Deployed an MCP server** (3 tools: index / search / get_document) so users can connect their own Claude/GPT
> - Fixed a production agent-stopping bug by gating deepagents auto-compaction output that broke the OpenUI parser

Why it works: every bullet has ownership + numbers + a named modern stack. "Evals + agents + MCP" is the rarest, most-demanded combo in the 2026 market (Anthropic has a "Model Evaluations" role; Microsoft lists benchmark suites/red-team; D.E. Shaw wants people who "build, evaluate, and deploy AI coding agents").

### 2. Add load-testing / performance engineering bullet (same role)
Satisfies the "production reliability" bar that finance AI roles (Jane Street, Two Sigma, D.E. Shaw) and SWE systems roles screen for.

> - Benchmarked a FastAPI + Postgres service with Locust: identified and fixed bottlenecks in order (connection pool, uvicorn workers, locust event loop, DB row-lock contention) → **~1000 RPS write at p95 577ms**; deployed indexes giving **+129.9% RPS (REST)** and **+33.6% (GraphQL)**; profiled to rule out ORM/pydantic — DB-bound

### 3. Add the auth / security bullet
Security closure reads better than "added auth"; security is a hot differentiator.

> - Added **Microsoft Entra ID bearer-token auth** to a FastAPI service exposed via the cluster edge — previously callable by any machine that could reach it (closed a genuine cluster-wide exposure)

### 4. Add the Kubernetes ops bullet
Matches the SWE cloud/infra cluster (cloud 53%, K8s 26%) with honest scope.

> - Debugged production issues on **Kubernetes** (Helm, Headlamp, kubectl, Datadog)

---

## P1 — STRONG ADDS (real signal, moderate effort)

### 5. 15 AI — compact founder entry (fills the Mar 2025–Apr 2026 timeline gap)
Founding-engineer × 13 months is real founder signal. **1–2 bullets max, never lead with it.**

> **15 AI** · Founding Engineer — Mar 2025 – Apr 2026
> - Built a search engine over scraped Key Opinion Leader data (contacts queryable by product/tag) and an Astro-based content site; owned product development end-to-end through rapid prototyping as the company iterated on direction

⚠️ Honesty flag: dates overlap Goodnotes (Jun–Sep 2025) and the placement's first month — mark part-time if applicable; a careful reader will notice.

### 6. Year 3 — include PROBE + robotics; skip the diffusion model as-is
- **PROBE** (the Computing Research Collective module) is a **public research artifact** — the counterweight to "no GitHub". Links to AI/ML roles directly.
  > Ongoing research benchmark (LemonPhase/PROBE) on how repo documentation structure affects coding-agent performance — SWE-bench-derived instances, runtime-validated
- **Robotics 2nd in cohort** shows leadership + hardware:
  > Led team to 2nd in cohort — object-avoiding path planning (Raspberry Pi, camera, Lego motors)
- **Diffusion model: skip or reframe.** "~98% classifier confidence" reads amateur without FID or a repo link (explicitly flagged in the research). If kept, needs a real metric + link; on a 1-pager, drop it.

### 7. Rewrite the Technical Skills section
Add the stack the market actually screens for (and that you genuinely have):
- **Add:** Kubernetes, LLM agents & evals (LangSmith), MCP, RAG/vector search (Manticore), Locust/performance testing, AI-assisted development (Cursor/Claude Code) — the AI-fluency signal is now *required* at ~6/19 SWE JDs and explicit at Meta/Microsoft
- **Keep:** Python, FastAPI, Docker, AWS, Postgres/SQL, TypeScript, React, PyTorch
- **Do NOT add:** C++ (you list C; claiming C++ for quant roles is interview-suicide — they test it), Go (not yet)

### 8. Education — one line for Year 3
Cheap ML-signal for AI roles:
> **Year 3: High First Class** — modules incl. Introduction to ML, Maths for ML, Deep Learning, Computer Vision, Robotics, Optimisation

### 9. Add GitHub links
Degrees are fading (11/19 SWE JDs omit); demonstrable work wins. At minimum:
- `github.com/LemonPhase` + direct link to **PROBE** on the projects/education line
- Only if space allows: jack-cv repo itself (meta, but shows craft)

---

## P2 — POLISH

### 10. Goodnotes — keep, minor tweaks only
Already quantified (2M+ users, 50k users, 750k weekly). One possible add: an AI-assisted-development note if a bullet needs refreshing. Do not touch the numbers.

### 11. Global framing principles (from the JD soft-skill data)
- **Every bullet = ownership + number + outcome.** Tier-3 quotes: "owning a problem over executing a ticket" (Pinecone), "from idea to production" (Anthropic), "slope over intercept" (Ramp)
- **Written communication is the most-quoted soft skill** — the CV itself is the proof; keep it ATS-crisp (already is)
- Lead the hedge fund entry with the agent, not the platform work — it is the differentiator
- Keep 1 page unless the two-page decision is made deliberately

### 12. Interview prep note (not CV content, but implied by the data)
- **AI/SWE interviews:** DSA + system design are tested even when JDs omit them (assumed). Practise both.
- **Quant dev interviews:** C++ is tested hands-on ("we will test" — Wintermute). Don't apply for C++-required quant-dev roles until you have real C++ evidence.
- **Go** is the #1 backend language in big-tech JDs (63%) — worth learning for the SWE path.

---

*Companion docs on this branch: `docs/placement-2026-worklog.md` (source material) · `docs/job-market-analysis-2026.md` (market evidence).*
