<h1 align="center">Sanjay Sakhinala</h1>

<p align="center">
  <b>AI/ML Engineer</b> — agentic RAG · LLM evaluation · reinforcement learning<br>
  Hyderabad, India · <b>Open to entry-level AI/ML and software engineering roles</b>
</p>

<p align="center">
  <a href="https://sanjaysakhinala.pages.dev"><img src="https://img.shields.io/badge/Portfolio-111111?style=flat-square&logo=google-chrome&logoColor=white"></a>
  <a href="https://linkedin.com/in/sanjaysakhinala"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white"></a>
  <a href="mailto:sanjaysakhinala@gmail.com"><img src="https://img.shields.io/badge/Email-333333?style=flat-square&logo=gmail&logoColor=white"></a>
  <a href="https://sanjaysakhinala.pages.dev/SanjayBhargav_Resume.pdf"><img src="https://img.shields.io/badge/Résumé-2E7D32?style=flat-square&logo=readthedocs&logoColor=white"></a>
</p>

---

I build LLM systems that can be **checked**, not just demoed — citation grounding, faithfulness
scoring, and evaluation harnesses that turn "the answer looks right" into a number you can
regress against. B.Tech ECE, 2025. Three papers, one patent, and one project I've been shipping
solo since November 2025.

**72%** fewer electromagnetic simulations via uncertainty-aware RL · **<2%** hallucination rate
on a 12-language RAG pipeline · **3** accepted papers · **1** Indian patent application

---

## Selected work

### [IndicRAG](https://github.com/DNSdecoded/IndicRAG) — multilingual agentic RAG

[![Last commit](https://img.shields.io/github/last-commit/DNSdecoded/IndicRAG?style=flat-square&label=active)](https://github.com/DNSdecoded/IndicRAG/commits)
[![Stars](https://img.shields.io/github/stars/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/stargazers)

Self-correcting research assistant across **12 languages** (English + 11 Indic), querying a local
corpus, arXiv, Semantic Scholar/OpenAlex, and the web in a single pipeline. LangGraph StateGraph —
planner → tool selector → executor → generator → reflexion evaluator — 6 tools, dual-gate verification.

> **Retrieval** BGE-M3 dense + BM25 fused with RRF (k=60), cross-encoder and ColBERT MaxSim reranking,
> NLI claim-level faithfulness checks.
> **Measured** Recall@5 **0.92** · citation grounding **0.94** · hallucination rate **under 2%**.
> **Ops** three-tier TTL/LRU cache, round-robin multi-key balancing, Prometheus, Nginx + Docker Compose.
> **Discipline** 100+ commits through v2.4.0 since Nov 2025 — PR review, semantic versioning, documented rollbacks.

`LangGraph` `BGE-M3` `ChromaDB` `Gemini` `FastAPI` `PyMuPDF` `Docker`

<br>

### [Meridian UM](https://github.com/DNSdecoded/meridian-um-platform) — AI-augmented prior authorization

Healthcare utilization-management reference implementation built on one rule: **no LLM output reaches
a human reviewer unsourced.**

> Citation grounding enforced at the schema level — every finding must resolve to a document span or
> policy-clause ID, uncited findings are rejected. A PostgreSQL `CHECK` constraint blocks any denial
> without a recorded human attestation. A property test fails if either invariant is weakened.
> Async FastAPI + SQLAlchemy 2.0 on PostgreSQL 16, pgvector policy-clause embeddings, 11-state
> forward-only case workflow, OCR span indexing, role gating, JWT.
> Offline eval harness reports accuracy, per-label P/R/F1, and citation validity over ~150 labeled cases.
> **Synthetic data only.**

`FastAPI` `SQLAlchemy 2.0` `PostgreSQL 16` `pgvector` `OCR` `Apache-2.0`

<br>

### [AgentOps](https://github.com/DNSdecoded/AgentOps) — agent observability & evaluation

A mini-LangSmith: records agent executions (planner → tool → retrieval → LLM) against a 12-table trace
schema and renders them as an interactive React Flow execution graph with per-node inspection.

> **Dual-path evaluation** zero-cost token-overlap heuristics by default, swappable to a Gemini judge —
> both return faithfulness, retrieval relevance, hallucination score, and unsupported-claim extraction.
> **Prompt Lab** A/B-tests prompt versions on success rate, cost, latency, and hallucination delta.
> **Safe by construction** the Python SDK buffers steps client-side and records exceptions as failed runs,
> so instrumentation never crashes the host app; all write paths are API-key gated against economic DoS
> through paid judge calls.

`FastAPI` `Next.js 14` `TypeScript` `PostgreSQL` `React Flow` `Python SDK`

<br>

### [RL for electromagnetic structure optimization](https://sanjaysakhinala.pages.dev/blog/rl-antenna-design.html) — accepted, WAMS 2026

Cut CST Studio simulation count by **72%** — ~1,500 GA-baseline calls down to **420**.

> Soft Actor-Critic trained 2.68M steps against a blended surrogate ensemble (2×LightGBM + MLP + RidgeCV,
> sub-5 ms inference), with uncertainty-aware reward shaping and an active-learning loop that re-simulates
> top candidates to limit model drift.
> **Beat all five baselines** (GA, PSO, DQN, PPO, DDPG) on a 28 GHz patch antenna: −52.2 dB return loss,
> 8.93% FBW, 5.272 dBi gain, 80.6% radiation efficiency — the only method in the comparison combining
> surrogate acceleration, uncertainty quantification, and fabrication constraints.
> Converged on a **quad-core CPU, no GPU**, using curriculum learning (32 → 64 → 128 step episodes) with VecNormalize.

`PyTorch` `Stable-Baselines3` `LightGBM` `Optuna` `CST API`

---

## Research

| | |
|---|---|
| **Uncertainty-Aware RL with Blended Surrogate Models for Electromagnetic Structure Optimization** | Accepted, WAMS 2026 — BVRIT Hyderabad |
| **Bandwidth Enhancement of Slotted Hexagonal Patch Antenna for 6G and BCI** | ICMOCE 2025, IIT Bhubaneswar — [DOI](https://doi.org/10.1109/ICMOCE64100.2025.11076991) |
| **Bandwidth Optimization of Slotted Circular Patch Antenna for 6G and BCI** | 16th ICCCNT 2025, IIT Indore — IEEE Xplore pending |
| **Patent — Design of Hexagonal Patch Antenna at 28 GHz** | Indian application No. 202541014595 A, published Mar 2025 |

---

## Toolkit

**Core** Python · SQL · PyTorch · FastAPI · PostgreSQL · Docker · Linux
**LLM & agents** LangGraph · LangChain · CrewAI · HuggingFace Transformers · RAG · multi-agent systems · LLM evaluation & observability · fine-tuning · multilingual embeddings · OCR
**ML & RL** scikit-learn · TensorFlow · LightGBM · Stable-Baselines3 · Optuna · OpenCV
**Data & infra** pgvector · ChromaDB · FAISS · Redis · SQLAlchemy 2.0 · MLflow · Prometheus · CI/CD · GCP / Vertex AI
**Analysis** pandas · NumPy · SciPy · Matplotlib · Streamlit

---

<details>
<summary><b>More projects</b> — multi-agent data science, Signal Protocol messenger, CNN remote sensing, DNS benchmarking</summary>

<br>

**[ai_data_scientist](https://github.com/DNSdecoded/ai_data_scientist)** — seven sequential CrewAI agents take a raw dataset to cleaned data, trained models, charts, and an executive report. Every agent is bound to deterministic pandas/scikit-learn/SciPy tools, so the LLM orchestrates while the tools compute — reproducible and cheap on tokens. SQLite experiment store, LiteLLM provider abstraction, exponential-backoff retry on HTTP 429.

**[CipherChat](https://github.com/DNSdecoded/CipherChat)** — end-to-end encrypted messenger implementing the Signal Protocol (X3DH key agreement + Double Ratchet) with AES-256-GCM, TLS transport, perfect forward secrecy, TOFU key verification, IPv4/IPv6.

**[landuse-cnn-eurosat](https://github.com/DNSdecoded/landuse-cnn-eurosat)** — 3-layer CNN trained from scratch in PyTorch: 89% test accuracy on 27,000 EuroSAT images across 10 classes (70/15/15 split). Grad-CAM hooks on the final Conv2d layer confirm the model keys on spatial structure rather than texture.

**[ResolverLab](https://github.com/DNSdecoded/ResolverLab)** — DNS benchmarking across 50+ filtered providers: block accuracy, latency, cache behaviour over UDP, TCP, DoH, DoT, with automated HTML reporting.

</details>

<details>
<summary><b>Training</b></summary>

<br>

| Program | Provider | Period |
|---|---|---|
| Generative AI | SkillHive Connect | Aug – Dec 2025 |
| AI/ML | Google for Developers | Jan – Mar 2025 |
| Cybersecurity | Palo Alto Networks | Oct – Dec 2024 |
| Data Science (RapidMiner) | Altair | Apr – Jun 2024 |

</details>

---

<p align="center">
  <b>Open to entry-level AI/ML and software engineering roles.</b><br>
  <a href="mailto:sanjaysakhinala@gmail.com">sanjaysakhinala@gmail.com</a> ·
  <a href="https://linkedin.com/in/sanjaysakhinala">LinkedIn</a> ·
  <a href="https://sanjaysakhinala.pages.dev">Portfolio</a>
</p>
