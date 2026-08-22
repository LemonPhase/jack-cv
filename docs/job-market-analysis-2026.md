# Job Market Analysis — Quant Dev / Software Engineer / AI Engineer

**Research date:** 2026-08-13 · **Data:** 76 real job descriptions, live-fetched from primary sources (two rounds: ATS-API round + browser gap-fill round)
**Prepared for:** Jack Zhang (CV targeting: AI Engineer / SWE / forward-deployed; quant/finance interest)
**Purpose:** evidence base for the `main.tex` rewrite — which skills and qualities the market actually demands, ordered by importance.

---

## 0. Methodology & data

- **76 real JDs** pulled **live from company-owned sources** (official ATS APIs, career pages, and browser-rendered career sites): Greenhouse, SmartRecruiters, Lever, Ashby, iCIMS, Workday, company sites (Google, Microsoft, Meta, Apple, D.E. Shaw, Jump, Optiver, G-Research, Wintermute, Two Sigma, Jane Street).
- **Zero** LinkedIn/Indeed summary pages — every JD is the actual posting text.
- Breakdown: **Quant/algotrading 32** · **SWE 20** · **AI/ML engineer 20** · **Google/big-tech cross-cuts 4** (see Appendix A for the full inventory with URLs).
- Company coverage:
  - **Quant/finance:** Jane Street, Point72/Cubist (×8), WorldQuant (×6), Virtu, IMC, SIG, Optiver, G-Research, D.E. Shaw (2), Jump Trading (5), Coinbase Trading, Wintermute, FalconX, Two Sigma, Jane Street ML
  - **Big tech:** Google (4), Microsoft (2), Meta (1), Apple (1), Amazon/AWS, Stripe, Airbnb, Datadog, Reddit, Pinterest, Roblox, Vercel, NVIDIA
  - **Startups:** Mercury, Linear, Pinecone, LangChain, Mistral, Notion, Ramp, OpenAI, Anthropic, Scale AI, Glean, Harvey, Together, Perplexity, Midjourney, Framer, Retool
- **Gap-fill round (browser):** Microsoft, Meta, Apple, D.E. Shaw, and Jump Trading were captured in a second pass using rendered-browser access (their APIs/raw HTML were blocked). Extracts archived at `/opt/data/tmp/jd_extra/gapfill_jds.md` (machine-local).
- **Remaining limitations (honest):** Citadel/Citadel Securities (Cloudflare challenge on both domains) and Millennium (careers site network-unreachable from this server) could not be captured. Patterns for those two are inferred from the other 14 quant firms captured.
- Frequency counts are per-category (quant 32, SWE 20, AI 20) — denominators differ; treat percentages as directional, not statistical.
- JDs emphasize required skills; interview reality (DSA weight) is inferred from stated "we will test" phrasing and known hiring bars.

---

## 1. QUANT DEVELOPER / ALGORITHMIC TRADING ENGINEER (27 JDs round 1; net 32 with gap-fill §6)

Firms: Jane Street, Point72/Cubist, WorldQuant, Virtu, IMC, SIG, Optiver, G-Research, Coinbase, Wintermute, FalconX, Two Sigma (+ D.E. Shaw, Jump in §6).

### Skill frequency (round 1, n = 24–27)
| Rank | Skill | Frequency | Where it sits |
|---|---|---|---|
| 1 | **C++** (often explicitly "low-latency C++") | **17/24 (71%)** | Required — tested in interview |
| 2 | **Low-latency / high-performance systems** | **15/24 (63%)** | Required mindset |
| 3 | **Python** | **13/24 (54%)** | Required in some, research/tooling complement in others |
| 4 | **Networking / client-server / exchange connectivity / FIX** | **12/24 (50%)** | Required |
| 5 | **Multithreading / concurrency** | **10/24 (42%)** | Required |
| 6 | **Linux** | **9/24 (38%)** | Required |
| 7 | **Data structures & algorithms** | **9/24 (38%)** | Interview-tested |
| 8 | **Market microstructure / trading domain** | **8/24 (33%)** | Usually preferred, sometimes required |
| 9 | **Probability / statistics / math** | **7/24 (29%)** | Required only in research-adjacent roles |
| 10 | Java (3), Go (2), OCaml (1) | ~12% | Firm-specific (Jane Street = OCaml) |

### Required vs preferred
- **Near-universal required:** C++, low-latency thinking, networking, Linux + multithreading, solid CS fundamentals.
- **Preferred/nice-to-have:** Python for non-Python roles; market microstructure; probability/stats; prior HFT/prop experience; personal projects; graduate degrees (math/CS/physics).
- **Experience bars:** mid-level ~2–4 yrs (Wintermute: "At least 2 years' experience with C++ — **we will test**"); senior 5–8+ (Optiver: "8+ years as a Quantitative Engineer working closely with traders and researchers").

### Soft skills / qualities (verbatim)
- Ownership/impact: Wintermute — *"get a lot of independence and responsibility right away… It is up to you to make an impact!"*; Optiver — *"Our engineers own problems end-to-end."*
- Collaboration with traders/researchers: Optiver — *"proven ability to successfully partner with traders and researchers"*, *"mentor and guide other members of the team"*.
- Intellectual curiosity / low ego: *"likes opening the hood to see how things work"* (Wintermute); Jane Street culture: *"intellectual curiosity", "low ego"*.
- Hands-on leadership: Optiver — *"This is a hands-on role. You will be expected to lead by example."*
- Speed/adaptability: *"features often reaching production within days"*; *"learn at an unprecedented speed"*.

### Notable patterns
1. **C++ is the unequivocal king** — even the crypto startup (Wintermute) tests C++ internals and networking.
2. **"Quant Developer" vs "SWE — Trading Systems" is blurred** — SIG's Core OMS Developer, IMC's C++ SWE, WorldQuant's SWE Trading Systems are quant-dev roles without the title. Don't title-match; match on C++/low-latency/networking.
3. **"We will test" is literal** — interview-validated practical skills carry heavy weight; DSA + systems interviews.
4. **AI/ML is creeping into quant-dev** (Point72 Quant Dev Trading Research; WorldQuant "Quant Research Intern (LLMs & AI Agents)") — Python + ML tooling increasingly preferred.
5. Firms are geographically diversifying (Budapest, Montevideo, Warsaw, Mumbai).

---

## 2. SOFTWARE ENGINEER — generalist / backend / infra (19 JDs round 1; net 20 with gap-fill §6)

Firms: Google (4), Amazon/AWS, Stripe, Airbnb, Datadog, Reddit, Pinterest, Roblox, Vercel, Jane Street SWE, Robinhood, Coinbase, Point72 Data; startups Mercury, Linear, Pinecone, LangChain, Mistral, Notion, Ramp (+ Microsoft in §6).

### Skill frequency (n = 19)
| Rank | Skill | Frequency | Notes |
|---|---|---|---|
| 1 | **Distributed systems** | **9/19 explicit (~14/19 implied, 74%)** | The dominant theme |
| 2 | **Go** | **12/19 (63%)** | Most common "one of" language; Go+Python dominant pairing |
| 3 | **Python** | **10/19 (53%)** | |
| 4 | **Testing** | **10/19 (53%)** | Required at ~9 |
| 5 | **Cloud (AWS/GCP/Azure)** | **~10/19 (53%)** | Required ~7, preferred 2 |
| 6 | **C++** | **8/19 (42%)** | Performance shops |
| 7 | **TypeScript/JS/Node** | **7/19 (37%)** | Fullstack/product roles |
| 8 | **Java** | **7/19 (37%)** | |
| 9 | **SQL / relational DBs** | **7/19 (37%)** | |
| 10 | **Kubernetes** | **5/19 (26%)** | Infra-heavy roles |
| 11 | **System design** (exact phrase) | **4/19 (8–10 with "design/architecture" equivalents)** | Interview-critical |
| 12 | Rust | 3/19 (16%) | Rising at performance shops |
| — | "Algorithms & data structures" (written) | **only 2/19** | Assumed — tested in interviews, not listed |
| — | Degree required (not "or equivalent") | **3/19** | 11/19 omit education entirely |
| — | **AI-tool fluency** | **relevant 16/19; explicitly required ~6** | Including new-grad roles |

### Required vs preferred
- Languages are "one or more of" lists; **Go+Python** dominant.
- Distributed systems required at 9, preferred only at 1. Cloud required ~7 / preferred 2.
- **Fintech/payments/domain experience: always preferred, never required** — transferable engineering wins.
- YoE bands are the dominant screen (<2 → 9+ years).
- AI-tool fluency now explicit: Notion (new-grad) — "familiarity with Cursor/Claude Code"; Datadog — "validate, critique, and refine AI-generated output".

### Soft skills / qualities (verbatim)
- Ownership/agency: *"High ownership mentality: self-directed, full-lifecycle builder"* (Linear); *"you prefer 'owning a problem' over 'executing a ticket'"* (Pinecone); *"We look for slope over intercept"* (Ramp).
- Curiosity/humility: *"Humble and unafraid to ask questions and admit mistakes"* (Jane Street).
- Product sense: *"you care about UX, speed, and polish, and you push back when something doesn't feel right"* (Linear).
- Leadership: *"mentor engineers and act as a force multiplier"* (Airbnb).

### Notable patterns
1. **AI fluency is mainstream** — relevant in 16/19 JDs; ~6 require demonstrated AI-tool use in daily workflow.
2. **"Algorithms & data structures" is rarely written** (2/19) — assumed, tested in interviews; JDs emphasize distributed systems/scale instead.
3. **Explicit "system design" wording is rare** (4/19) — companies write "design or architecture (design patterns, reliability and scaling)".
4. **Degrees are fading** — 11/19 omit; Point72 is the strictest holdout.
5. **Rust rising** at performance shops; Jane Street/Point72 screen purely on problem-solving, curiosity, humility.
6. US postings universally include salary ranges (Airbnb $212–265k; Roblox new-grad $153k).

---

## 3. AI ENGINEER / ML ENGINEER / APPLIED AI (15 JDs round 1; net 20 with gap-fill §6)

Firms: OpenAI, Anthropic, NVIDIA, Amazon AGI, Scale AI (×2), Mistral (×2), Glean, LangChain, Harvey, Two Sigma, Jane Street ML, Together, Perplexity, Point72 ML (+ Microsoft, Apple, Meta, D.E. Shaw, Jump in §6).

### Skill frequency (n = 15)
| Rank | Skill | Frequency | Notes |
|---|---|---|---|
| 1 | **Python** | **13/15 (87%)** | Near-universal; TS alongside for applied roles |
| 2 | **ML fundamentals + strong CS/software-engineering rigor** | **12/15 (80%)** | Probability, statistics, model evaluation, ML system design |
| 3 | **LLM-specific experience** (APIs, prompt design, LLM app patterns, training/RL) | **11/15 (73%)** | Required at frontier labs; preferred at big-tech/finance |
| 4 | **Deep-learning framework (PyTorch/TF/JAX)** | **10/15 (67%)** | "At least one" — required at labs |
| 5 | **Production / deployment / shipping to users** | **10/15 (67%)** | Explicit in 10 |
| 6 | **Evals / benchmarking / evaluation-driven dev** | **8/15 (53%)** | Now a *named job function* ("Model Evaluations" teams) |
| 7 | **Agents / agentic systems / tool use** | **8/15 (53%)** | |
| 8 | **Distributed training / post-training (RLHF, SFT, DPO)** | **6/15 (40%)** | Research-engineer roles |
| 9 | **RAG / retrieval / search** | **5/15 (33%)** | |

### Required vs preferred
- **Hard requirements (universal):** Python + production software-engineering experience. Mid-level: 3+ yrs SWE (Amazon verbatim: *"3+ years of non-internship professional software development experience"*).
- **Preferred/plus:** PyTorch specifics (required at labs); explicit LLM experience (required at OpenAI/Anthropic/Scale/Glean/LangChain/Harvey; *preferred* at Amazon AGI/Jane Street/Two Sigma); advanced degrees (preferred at labs, explicitly NOT required at Scale/Jane Street/LangChain); Rust/Go for infra-near roles; GPU/CUDA/vLLM/inference-optimization (Together, NVIDIA).
- **Pattern:** Frontier-lab "Research Engineer" = deep-learning chops required; big-tech ML (Amazon/Jane Street) = ML is one track of a broader SWE bar.

### Soft skills / qualities (verbatim)
- **Written communication — literally everywhere.** NVIDIA's top bullet: *"strong written communication skills"*; OpenAI: *"excellent written communication"*; Two Sigma: *"the judgment to figure out what to build… and the communication to make it real."*
- Ownership/end-to-end: Anthropic — *"take ownership of projects from idea to production"*; Scale — *"ship fast", "love building"*; Two Sigma — *"This is not a research role… It is a building role."*
- Collaboration: customers + eng (Anthropic Applied AI), research/eng/safety (Harvey), traders + engineers (Jane Street).
- Curiosity/growth: OpenAI — *"excited to learn"*; NVIDIA — *"ability to learn new domains quickly"*; LangChain — *"write to learn and to teach."*
- Product sense/judgment: Two Sigma — *"the judgment to figure out what to build"*; Mistral — *"comfort with ambiguity."*

### Notable patterns
1. **"Applied AI Engineer" is now a distinct, widely-advertised role family** (OpenAI, Anthropic, Mistral, Scale, Ramp, Stripe, LangChain) — centers on LLM APIs, agents, **evals**, and *deployment to customers*, not model training.
2. **Agents + evals + post-training are core job titles/lines**, not niche: Anthropic "Research Engineer, Model Evaluations"; Harvey "Research Engineer, Post-Training"; Scale "Frontier Agents Engineer"; OpenAI "Applied AI Engineer, Codex Core Agent".
3. **Finance/quant AI roles (Jane Street, Two Sigma, Point72) look like strong-SWE + ML** rather than startup "LLM app" jobs: production reliability, CS fundamentals, trading-domain ML.
4. **Communication and ownership appear before tech stacks in several JDs** (NVIDIA, LangChain, Mistral).

---

## 4. CROSS-CUTTING SYNTHESIS — skills & qualities ordered by importance

### Tier 0 — Table stakes, every role, every company type
1. **Strong CS fundamentals** (data structures, algorithms, complexity) — *rarely written, always interview-tested* (Google 3/4 JDs list DSA; Wintermute "we will test"; Jane Street screens purely on problem-solving).
2. **Software-engineering rigor** — clean code, testing, code review, debugging discipline (testing required in ~10/19 SWE JDs; "production software development experience" is the universal bar).
3. **Communication** — written communication is the single most-quoted soft skill across all 76 JDs (NVIDIA top bullet; OpenAI "excellent written communication"; Two Sigma "communication to make it real").

### Tier 1 — Role-defining core (pick your lane)
| Quant Dev | SWE (big tech/startup) | AI Engineer |
|---|---|---|
| **C++ (71%)** | **Distributed systems (74%)** | **Python (87%)** |
| **Low-latency systems (63%)** | **Go (63%)** / Python (53%) | **ML fundamentals + SWE rigor (80%)** |
| **Networking/FIX (50%)** | **Cloud AWS/GCP/Azure (53%)** | **LLM stack: APIs, prompts, agents, evals (73%)** |
| **Multithreading (42%), Linux (38%)** | **Testing (53%), SQL (37%)** | **PyTorch/TF/JAX (67%)** |
| **DSA (38%, interview)** | **System design (interview-critical)** | **Production/deployment (67%)** |

### Tier 2 — Differentiators (turn good → hired)
- **Quant dev:** market microstructure/trading domain (33%), probability/stats (29%), HFT/prop experience, personal projects.
- **SWE:** Rust (16%, rising), Kubernetes (26%), Kafka/streaming, fintech domain (always preferred), **AI-tool fluency (required at ~6/19 — new)**, system-design depth at scale.
- **AI engineer:** evals/benchmarking engineering (53% — now a named function), agents/tool use (53%), distributed training/post-training (40%), RAG/retrieval (33%), MLOps/serving (vLLM/CUDA).

### Tier 3 — Qualities that decide offers (verbatim-weighted)
1. **Ownership / end-to-end / builder mindset** — appears in all three categories ("owning a problem over executing a ticket" Pinecone; "own problems end-to-end" Optiver; "from idea to production" Anthropic; "It is a building role" Two Sigma).
2. **Intellectual curiosity + humility / low ego / learn-fast** — Jane Street, OpenAI ("excited to learn"), Wintermute ("opening the hood").
3. **Collaboration across roles** — with traders (quant), with customers (applied AI), with cross-functional teams (SWE) — plus mentorship at senior levels ("force multiplier", "mentor and guide").
4. **Judgment / ambiguity tolerance / product sense** — Two Sigma "the judgment to figure out what to build"; Mistral "comfort with ambiguity"; Linear "you push back when something doesn't feel right".
5. **Speed / bias for action** — "slope over intercept" (Ramp), "ship fast" (Scale), "production within days" (Optiver).

### Market signals (2026)
- **AI fluency is now baseline for SWE** — even new-grad JDs mention Cursor/Claude Code; "validate/critique AI output" is a required skill at Datadog.
- **Evals has become a standalone engineering discipline** — a huge tailwind for anyone with real eval harness experience.
- **Degrees are fading** (11/19 SWE JDs omit); YoE bands + demonstrable impact dominate.
- **Go+Python is the big-tech backend pairing; C++ is non-negotiable for quant; Python is non-negotiable for AI.**
- **Rust rising; distributed systems > "algorithms" in JD text** (but DSA still interview-tested).

---

## 5. WHAT THIS MEANS FOR JACK'S CV (data-grounded)

**His strongest alignment: AI Engineer / Applied AI** — the AI JDs read like his placement:
- Python + production FastAPI services ✓
- LLM agents (langchain deepagents), MCP server ✓ (MCP is literally what OpenAI/Anthropic/Scale build with)
- **Evals engineering** (LangSmith harness, recall/recency, −90% tokens/0% recall impact) — matches a *named job function* at Anthropic/Glean/Microsoft; genuinely rare for a new grad
- Production deployment + load-testing at scale (~1000 RPS, p95 577ms) — satisfies the "production/reliability" bar that finance AI roles (Jane Street, Two Sigma, D.E. Shaw) demand
- **Gaps to close for AI roles:** PyTorch depth (he has PyTorch on CV but no flagship ML project beyond coursework — the diffusion model is weak as phrased); ML fundamentals vocabulary (probability/stats framing); a public artifact (PROBE repo is the counterweight).

**SWE path:** strong on Python/TS, Docker, AWS, FastAPI, testing; **gaps:** Go (12/19 JDs), distributed-systems depth at scale (his load-testing story helps), Kafka/streaming, system-design interview prep. The hedge-fund platform work (Dagster pipelines, K8s debugging via Helm/kubectl/Datadog) directly matches the "cloud + distributed + testing" cluster.

**Quant dev path:** this is the steepest ask — C++ is 71% required and *interview-tested* ("we will test"); he lists C (not C++) on the CV; low-latency/networking/multithreading are core, and his placement is application-layer. His math record (A\*A\*A\*A, Imperial, Optimisation/KKT) helps only for research-adjacent roles. **If quant dev is a real target:** invest in C++ systems programming + networking + concurrency (visible projects), and expect a systems-grilling interview. The CV should NOT claim quant-dev without C++ evidence. Note the title-blurring: "SWE — Trading Systems" roles are the same profile.

**Cross-cutting CV actions (from the data):**
1. Lead with **ownership + numbers** — every tier-3 quote is about end-to-end ownership; his bullets already do this (keep the "game changer", 130k corpus, −70% tokens numbers).
2. Put **evals + agents + MCP** front and center for AI roles — it's the single rarest, most-demanded combo in the 2026 market.
3. **Written communication** is the top-quoted soft skill — the CV itself and any cover letter must be crisp; his CV is already ATS-clean.
4. **AI-tool fluency** should be explicit (Cursor/Claude Code/deepagents usage) — new-grad JDs literally ask for it.
5. For finance/quant targets, frame the placement as *production reliability + performance engineering* (load-testing, p95, index optimization) — matches what Jane Street/Two Sigma/D.E. Shaw ML JDs screen for.

---

## 6. GAP-FILL ROUND — NEW CAPTURES & REVISED SIGNALS (browser pass)

Round 2 added 11 JDs from the previously-blocked firms. Full extracts: `/opt/data/tmp/jd_extra/gapfill_jds.md` (machine-local).

### Newly captured (all primary, fetched 2026-08-13)
| Company | Role | Key requirements |
|---|---|---|
| **Microsoft** | Senior SWE, M365 Fleet Health | BS + 4+ yrs (C/C++/C#/Java/JS/Python); **distributed systems at scale**; telemetry analytics (Kusto/Spark/Databricks); ML/anomaly detection; AI agents for ops; $119.8–234.7k |
| **Microsoft** | Senior AI Engineer, Security AI | BS + 4+ yrs; **LLMs, agentic workflows, RAG, knowledge graphs**; **evaluation frameworks, benchmark suites, red-team, human-eval frameworks**; agents/multi-agent; vector search/retrieval/memory; prompt-injection defense; explain to non-technical audiences |
| **Meta** | Staff SWE, Systems ML | 8+ yrs systems/distributed/ML infra; **C++/Python**; profiling/SLOs; **AI-assisted dev workflows required**; pref: PyTorch distributed training, GPU/CUDA, **prompt/context engineering + agent orchestration**, OSS ML contributions |
| **Apple** | Sr ML Engineer, Foundation Models Inference | 5+ yrs end-to-end; **LLM inference stacks**; GPU/TPU; PyTorch/JAX/TF; high-throughput at scale; K8s/Docker; pref: Go/Python, **vLLM/SGLang/TensorRT-LLM/Triton**, custom CUDA kernels |
| **D.E. Shaw** | Software Developer (Quant Strategies) | Statistical models for trading; **distributed systems reacting to data in real time**; math-modeling tools; "top students + extensive SWE experience"; **base $275k + guaranteed year-1 bonus** |
| **D.E. Shaw** | Applied AI Engineer | **Bespoke AI agents + agentic frameworks (orchestration, tool use, memory, multi-step reasoning in production)**; eval AI coding agents; retrieval at scale; greenfield concept→production; degree-agnostic (any field) + strong SWE |
| **Jump** | Quantitative Developer ×2 (NYC/Chi, HK) | **Python AND C++** prod systems; live trading ops reliability; large data sets; ownership; works with researchers |
| **Jump** | SWE (NYC/Chi) + SWE Market Data | 5+ yrs **Python distributed systems**, Linux; real-time streaming, low latency, market data |
| **Jump** | Research Engineer, Pre-Training | Foundation models for trading; training infra across **thousands of GPUs/TPUs**; custom kernels; mixed-precision; model parallelism |

### What the gap-fill changes in the analysis
1. **Big-tech SWE pattern confirmed at Microsoft/Meta**: distributed systems + cloud + testing + **AI-assisted development is now explicitly required** (Meta: "Leverage AI-assisted development workflows... applying sound judgment on when to rely on AI tooling"; Microsoft Fleet Health: "Build AI-assisted experiences"). The AI-fluency signal strengthens from "relevant 16/19" to a genuine big-tech hiring requirement.
2. **Evals/benchmarking is a first-class skill at the very top**: Microsoft Security AI lists "evaluation frameworks, benchmark suites, red-team methodologies, human evaluation frameworks" in preferred quals; D.E. Shaw Applied AI = "build, **evaluate**, and deploy AI coding agents"; Meta prefers "experimentation frameworks". This cements the earlier finding: eval engineering is a distinct, highly-demanded discipline.
3. **Quant dev = C++ still, but Python+distributed is the new second track**: Jump's Quant Dev requires **Python AND C++**; Jump's generic SWE is pure Python + distributed systems; D.E. Shaw SWE is language-agnostic with heavy systems focus. C++ remains the differentiator for latency-critical roles (Market Data streaming, OMS, exchange connectivity), but pure-Python systems roles exist at the same firms.
4. **Frontier ML is now inside quant firms**: Jump's Research Engineer, Pre-Training (foundation models over market data, GPU/TPU scale) and D.E. Shaw's Applied AI Engineer are mainstream quant hiring — Jack's LLM-agent + eval background is directly relevant to the finance AI bucket, not just startup AI.
5. **Comp benchmarks (US)**: D.E. Shaw SWE base $275k + guaranteed bonus; Microsoft IC4 $119.8–234.7k; Airbnb Staff $212–265k; Roblox new-grad $153k — quant pays a clear premium at the top end.
6. **Degree requirements are loosening even at finance**: D.E. Shaw Applied AI explicitly accepts "a bachelor's degree in any field" with strong SWE experience — consistent with the broader market signal that demonstrated work > degree.

### Updated tier-1 cores (with gap-fill incorporated)
| Quant Dev (~32) | SWE (~20) | AI Engineer (~20) |
|---|---|---|
| **C++ (interview-tested)** | **Distributed systems (dominant)** | **Python (near-universal)** |
| **Python + prod systems** (Jump HK explicitly both) | **Go + Python pairing** | **ML fundamentals + SWE rigor** |
| **Low-latency / real-time streaming** | **Cloud + testing** | **LLM stack: agents, RAG, evals** |
| **Networking / market data / FIX** | **K8s, SQL, system design** | **PyTorch + production/deployment** |
| Multithreading, Linux | Rust rising, AI fluency | **Evals/benchmarking (now a named discipline)**, inference (vLLM/CUDA) |

---

## 7. LIMITATIONS
- **Citadel/Citadel Securities** (Cloudflare challenge on www.citadel.com and www.citadelsecurities.com) and **Millennium** (careers site network-unreachable) remain the only named-gap firms; their quant-dev hiring patterns are corroborated by the other 14 quant firms captured (including two direct peers: D.E. Shaw and Jump).
- Frequency counts are per-category (quant 32, SWE 20, AI 20) — denominators differ; treat percentages as directional, not statistical.
- JDs emphasize required skills; interview reality (DSA weight) is inferred from stated "we will test" phrasing and known hiring bars.
- All other originally-blocked firms (Microsoft, Meta, Apple, D.E. Shaw, Jump) were captured in the browser gap-fill round — see Section 6.

---

## Appendix A — Full JD inventory (76 roles, all primary sources, fetched 2026-08-13)

### A1. Quant / algorithmic trading (32)
| # | Company | Role | Level / Location | Source |
|---|---|---|---|---|
| 1 | Jane Street | Low-Latency Engineer | Experienced / NY | boards.greenhouse.io/janestreet (id 6254435002) |
| 2 | Jane Street | Software Engineer | Experienced / NY | boards.greenhouse.io/janestreet (id 8599644002) |
| 3 | Point72 (Cubist) | Quantitative Developer | Experienced / HK | boards.greenhouse.io/point72 (id 7666604002) |
| 4 | Point72 (Cubist) | Quantitative Developer | Experienced / London | boards.greenhouse.io/point72 (id 8191564002) |
| 5 | Point72 (Cubist) | Quantitative Developer | Experienced / Chicago | boards.greenhouse.io/point72 (id 7297511002) |
| 6 | Point72 (Cubist) | Quantitative Software Developer | Experienced / NY | boards.greenhouse.io/point72 (id 8036928002) |
| 7 | Point72 (Cubist) | Low-Latency Market Data Engineer | Experienced / NY, London | boards.greenhouse.io/point72 (id 8050478002) |
| 8 | Point72 | Fund Flow Quantitative Developer | Mid / NY, Stamford | boards.greenhouse.io/point72 (id 8389369002) |
| 9 | Point72 (Cubist) | Quantitative Developer, Trading Research | Experienced / Warsaw | boards.greenhouse.io/point72 (id 8561446002) |
| 10 | Point72 | Quantitative Analyst / Software Developer | Mid / NY | boards.greenhouse.io/point72 (id 7297622002) |
| 11 | Virtu | SWE — Client Trading Infrastructure (Java) | Experienced / NY | boards.greenhouse.io/virtu (id 6072565002) |
| 12 | WorldQuant | Low Latency C++ Developer | Experienced / Budapest | boards.greenhouse.io/worldquant (id 4649328006) |
| 13 | WorldQuant | Quantitative Developer | Experienced / London | boards.greenhouse.io/worldquant (id 4659364006) |
| 14 | WorldQuant | Quantitative Developer | Experienced / CT, NY | boards.greenhouse.io/worldquant (id 4700347006) |
| 15 | WorldQuant | Quantitative Python Developer | Experienced / Montevideo | boards.greenhouse.io/worldquant (id 4379256006) |
| 16 | WorldQuant | Execution Developer | Experienced / NY, CT, Chi, Austin | boards.greenhouse.io/worldquant (id 4070178006) |
| 17 | WorldQuant | SWE — Trading Systems | Experienced / NY, Chi, Austin, CT | boards.greenhouse.io/worldquant (id 4062126006) |
| 18 | IMC | C++ Software Engineer | Experienced / Chicago, NY | boards.greenhouse.io/imc (id 4673650101) |
| 19 | IMC | Core Developer — Digital Assets | Experienced / Zug | boards.greenhouse.io/imc (id 4637267101) |
| 20 | SIG | Software Developer — Core Order Mgmt System (C++) | Experienced | careers.sig.com/jobs/11068 |
| 21 | SIG | Python Developer — Quant Core Data | Experienced | careers.sig.com/jobs/11163 |
| 22 | SIG | Senior Software Engineer — Research Tech | Senior | careers.sig.com/jobs/10085 |
| 23 | Optiver | Lead Quantitative Engineer | Senior (8+ yrs) / Mumbai | optiver.com/join-us/jobs/technology/mumbai/lead-quantitative-engineer/ |
| 24 | G-Research | C++ Software Engineer | Experienced / London | gresearch.com/vacancies/c-software-engineer-2/ |
| 25 | Coinbase | Senior SWE — Trading | Senior / Singapore | boards.greenhouse.io/coinbase (id 7866674) |
| 26 | Wintermute | C++ Quant Developer | Mid (2+ yrs C++) / London | wintermute.com/company/opportunities/ |
| 27 | FalconX | Sr. Infra Engineer — Trading Systems | Senior / NYC | boards.greenhouse.io/falconx (id 4719441005) |
| 28 | D.E. Shaw | Software Developer (Quantitative Strategies) | All levels / NY | deshaw.com/careers/software-developer-2646 |
| 29 | Jump Trading | Quantitative Developer — Trading Team | Experienced / NYC, Chicago | jumptrading.com/hr/job?gh_jid=7767735 |
| 30 | Jump Trading | Quantitative Developer | Experienced / HK | jumptrading.com/hr/job?gh_jid=7822791 |
| 31 | Jump Trading | Software Engineer | 5+ yrs / NYC, Chicago | jumptrading.com/hr/job?gh_jid=7156979 |
| 32 | Jump Trading | SWE — Market Data Systems | Experienced / Chicago | jumptrading.com/hr/job?gh_jid=7847009 |

### A2. Software Engineer (20)
| # | Company | Role | Level | Source |
|---|---|---|---|---|
| 1 | Stripe | Backend Engineer, Core Technology | Mid–Senior | Greenhouse (stripe) |
| 2 | Airbnb | Staff Backend Engineer, Ads Platform | Staff | Greenhouse (airbnb) |
| 3 | Datadog | Sr SWE, Distributed Systems | Senior | Greenhouse (datadog) |
| 4 | Reddit | Sr SWE, Core Platform | Senior | Greenhouse (reddit) |
| 5 | Pinterest | SWE II Backend | Mid | Greenhouse (pinterest) |
| 6 | Roblox | Early Career SWE (2027) | New grad | Greenhouse (roblox) |
| 7 | Vercel | SWE Backend | Mid | Greenhouse (vercel) |
| 8 | Amazon/AWS | SDE | Mid–Senior | Amazon jobs API |
| 9 | Jane Street | Software Engineer (full-time) | Experienced / NY | boards.greenhouse.io/janestreet (id 8594541002) |
| 10 | Robinhood | SWE Backend | Mid | Greenhouse (robinhood) |
| 11 | Coinbase | Sr SWE, Core Cryptography | Senior | Greenhouse (coinbase) |
| 12 | Point72 | SWE — Data | Mid | Greenhouse (point72) |
| 13 | Mercury | SWE Product | Series C | Ashby (mercury) |
| 14 | Linear | Sr/Staff Fullstack | Series C | Ashby (linear) |
| 15 | Pinecone | Sr/Staff | Series C | Ashby (pinecone) |
| 16 | LangChain | Sr Backend | Series B | Ashby (langchain) |
| 17 | Mistral | SWE New Grad | Series B | Ashby (mistral) |
| 18 | Notion | Early Career AI | New grad | Ashby (notion) |
| 19 | Ramp | SWE Core Product | Series D | Ashby (ramp) |
| 20 | Microsoft | Senior SWE, M365 Fleet Health | Senior / Redmond | jobs.careers.microsoft.com/global/en/job/200045384/ |

### A3. AI / ML / Applied AI (20)
| # | Company | Role | Level | Source |
|---|---|---|---|---|
| 1 | OpenAI | Research Engineer, Retrieval & Search | Mid / SF | Ashby (openai) |
| 2 | OpenAI | Applied AI Engineer, Enterprise | Mid / SF | Ashby (openai) |
| 3 | Anthropic | Applied AI Engineer, Enterprise Tech | Mid | Greenhouse (anthropic) |
| 4 | Anthropic | ML Infrastructure Engineer, Safeguards Research | Mid | Greenhouse (anthropic) |
| 5 | NVIDIA | Machine Learning Engineer, AI Safety | Mid / Santa Clara | Workday API |
| 6 | Amazon | MLE II, AGI Customization | Mid / Boston | Amazon jobs API |
| 7 | Scale AI | ML Research Engineer, Agents | Mid | Greenhouse (scaleai) |
| 8 | Scale AI | Staff Frontier Agents Engineer | Senior/Staff | Greenhouse (scaleai) |
| 9 | Mistral AI | Applied AI Engineer, Prototyping | Mid / Paris | Ashby (mistral) |
| 10 | Mistral AI | AI Engineer, Product | Mid / Paris | Ashby (mistral) |
| 11 | Glean | MLE, Assistant Quality | Mid / SF | Greenhouse (glean) |
| 12 | LangChain | AI Engineer, Enablement | Mid / SF | Ashby (langchain) |
| 13 | Harvey | Research Engineer, Post-Training | Mid / SF | Ashby (harvey) |
| 14 | Two Sigma | AI Solutions Developer | Mid–Senior / NYC | iCIMS careers portal |
| 15 | Jane Street | Machine Learning Engineer | Experienced / NY | janestreet.com jobs API |
| 16 | Microsoft | Senior AI Engineer, Security AI | Senior | jobs.careers.microsoft.com/global/en/job/200045144/ |
| 17 | Apple | Sr MLE, Foundation Models Inference | Senior / Seattle, Santa Clara | jobs.apple.com/en-us/details/200677962-3337/ |
| 18 | Meta | Staff SWE, Systems ML | Staff | metacareers.com/profile/job_details/2136998990191804 |
| 19 | D.E. Shaw | Applied AI Engineer | Experienced / NY | deshaw.com/careers/applied-ai-engineer-5375 |
| 20 | Jump Trading | Research Engineer, Pre-Training | Experienced / NY, London, Chicago | jumptrading.com/hr/job?gh_jid=7977686 |

### A4. Big-tech cross-cuts (4 — Google, captured via careers HTML)
| # | Company | Role | Level | Source |
|---|---|---|---|---|
| 1 | Google | Software Engineer, Full Stack (Pixel Weather) | Mid (2+ yrs) | careers.google.com (id 92162448210961094) |
| 2 | Google | Staff Software Engineer, Network Health | Staff (8+ yrs) | careers.google.com (id 123298905428239046) |
| 3 | Google | Senior SWE, Embedded Systems, Platforms & Devices | Senior (5+ yrs) | careers.google.com (id 79935621212054214) |
| 4 | Google | Software Engineer III, AI/ML, Display Ads | Mid (2+ yrs, C++ & Python) | careers.google.com (id 138233070430888646) |

---

## Appendix B — Compensation benchmarks (from JD-stated ranges, US)
- **D.E. Shaw** Software Developer (NY): base **$275,000** + substantial variable comp (year-end bonus **guaranteed in year 1**), sign-on, relocation
- **Microsoft** Senior SWE IC4: $119,800 – $234,700
- **Airbnb** Staff Backend: $212,000 – $265,000
- **Roblox** Early Career (new grad): ~$153,000
- Most US postings include ranges; quant compensation is heavily bonus-weighted and materially higher at the top end than big-tech base+equity for equivalent seniority.

---

## Appendix C — Raw data archive (machine-local, not in repo)
- `/opt/data/jds/` — SWE + AI JD extracts, full report `SWE_JD_ANALYSIS.md`, API JSON dumps (Greenhouse/Ashby/Lever/Amazon/NVIDIA/Workday)
- `/opt/data/jd_research/` — quant-dev round: 27 individual JD texts (`jd_*.txt`), consolidated `extracted_jds.json`, raw ATS dumps
- `/opt/data/tmp/jd_extra/` — Google ×4, Microsoft ×2, Meta, Apple, D.E. Shaw ×2, Jump ×5 extracts (`gapfill_jds.md` + JSON/HTML dumps)

*Companion doc: `docs/placement-2026-worklog.md` (Jack's placement + CV source material) on the same branch.*
