<div align="center">

# Sanjay Sakhinala

### AI/ML Engineer — Agentic RAG, LLM Evaluation & Reinforcement Learning
*Hyderabad, India · Open to entry-level AI/ML and software engineering roles*

[![Portfolio](https://img.shields.io/badge/Portfolio-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://sanjaysakhinala.pages.dev)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/sanjaysakhinala)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sanjaysakhinala@gmail.com)
[![Resume](https://img.shields.io/badge/Resume-2E7D32?style=for-the-badge&logo=readthedocs&logoColor=white)](https://sanjaysakhinala.pages.dev/SanjayBhargav_Resume.pdf)

</div>

---

## About

AI/ML engineer building agentic RAG systems, LLM evaluation tooling, and reinforcement
learning for engineering optimization. B.Tech in Electronics & Communication Engineering
(2025), now working full-time on production ML systems.

The work I care most about is **making LLM systems verifiable** — citation grounding,
faithfulness scoring, and evaluation harnesses that turn "the answer looks right" into a
number you can regress against.

Two things worth knowing:

- **IndicRAG** has been under continuous solo development since November 2025 — 100+ commits
  through **v2.4.0**, PR-based review workflow, semantic versioning, documented rollback
  procedures. It is the closest thing I have to a production on-call log.
- **Uncertainty-aware RL for electromagnetic design** cut CST simulation count by **72%**
  (~1,500 → 420 evaluations) and outperformed GA, PSO, DQN, PPO, and DDPG on a 28 GHz patch
  antenna — on a quad-core CPU, no GPU. Accepted at WAMS 2026.

---

## Featured Work

### 🔷 [IndicRAG](https://github.com/DNSdecoded/IndicRAG) — Multilingual Agentic RAG
[![Stars](https://img.shields.io/github/stars/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/stargazers)
[![Last commit](https://img.shields.io/github/last-commit/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/commits)
[![Commits](https://img.shields.io/github/commit-activity/t/DNSdecoded/IndicRAG?style=flat-square&label=commits)](https://github.com/DNSdecoded/IndicRAG/commits)
[![License](https://img.shields.io/github/license/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/blob/main/LICENSE)

Self-correcting research assistant across **12 languages (English + 11 Indic)**, querying a
local corpus, arXiv, Semantic Scholar/OpenAlex, and the web in one pipeline. LangGraph
StateGraph — planner → tool selector → executor → generator → reflexion evaluator — with
6 tools and dual-gate verification.

**Retrieval:** BGE-M3 dense + BM25 with RRF (k=60), cross-encoder and ColBERT MaxSim reranking,
NLI-based claim-level faithfulness verification.
**Measured:** Recall@5 0.92, citation grounding 0.94, under 2% hallucination rate.
**Ops:** three-tier TTL/LRU caching, round-robin multi-key load balancing, Prometheus metrics,
Nginx + Docker Compose.

`LangGraph` · `BGE-M3` · `ChromaDB` · `Gemini` · `FastAPI` · `PyMuPDF` · `Docker`

---

### 🔷 [Meridian UM](https://github.com/DNSdecoded/meridian-um-platform) — AI-Augmented Prior Authorization
[![Last commit](https://img.shields.io/github/last-commit/DNSdecoded/meridian-um-platform?style=flat-square)](https://github.com/DNSdecoded/meridian-um-platform/commits)
[![License](https://img.shields.io/github/license/DNSdecoded/meridian-um-platform?style=flat-square)](https://github.com/DNSdecoded/meridian-um-platform/blob/main/LICENSE)

Healthcare utilization-management reference implementation where **no LLM output reaches a
human reviewer unsourced**. Citation grounding is enforced at the schema level — findings must
resolve to a document span or policy-clause ID, uncited findings are rejected — and a
PostgreSQL `CHECK` constraint blocks any denial lacking a recorded human attestation. A
property test fails if either invariant is weakened.

Async FastAPI + SQLAlchemy 2.0 over PostgreSQL 16 with pgvector policy-clause embeddings, an
11-state forward-only case workflow, OCR span indexing, hierarchical role gating, and JWT
verification. Offline eval harness reports accuracy, per-label P/R/F1, and citation validity
over ~150 labeled synthetic cases. **Synthetic data only.**

`FastAPI` · `SQLAlchemy 2.0` · `PostgreSQL 16` · `pgvector` · `OCR` · `Apache-2.0`

---

### 🔷 [AgentOps](https://github.com/DNSdecoded/AgentOps) — LLM Agent Observability & Evaluation
[![Last commit](https://img.shields.io/github/last-commit/DNSdecoded/AgentOps?style=flat-square)](https://github.com/DNSdecoded/AgentOps/commits)

A mini-LangSmith. Records agent executions (planner → tool → retrieval → LLM) against a
12-table trace schema, renders them as an interactive React Flow execution graph with per-node
inspection, and rolls up per-model cost and per-stage latency.

Dual-path evaluation engine: zero-cost token-overlap heuristics by default, swappable to a
Gemini LLM judge — both return faithfulness, retrieval relevance, hallucination score, and
unsupported-claim extraction. Prompt Lab A/B-tests versions on success rate, cost, latency, and
hallucination delta. The Python tracing SDK buffers steps client-side and captures exceptions
as failed runs, so instrumentation never crashes the host application. All write paths are
API-key gated to prevent economic denial-of-service via paid judge calls.

`FastAPI` · `Next.js 14` · `TypeScript` · `PostgreSQL` · `React Flow` · `Python SDK`

---

### 🔷 [RL for Electromagnetic Structure Optimization](https://sanjaysakhinala.pages.dev/blog/rl-antenna-design.html) — Accepted, WAMS 2026

Cut CST Studio simulation count **72%** (~1,500 GA-baseline calls → 420) by training a Soft
Actor-Critic agent over 2.68M steps against a blended surrogate ensemble (2×LightGBM + MLP +
RidgeCV, sub-5 ms inference) with uncertainty-aware reward shaping and an active-learning loop
that re-simulates top candidates to limit model drift.

Outperformed all five benchmark optimizers (GA, PSO, DQN, PPO, DDPG): −52.2 dB return loss,
8.93% FBW, 5.272 dBi gain, 80.6% radiation efficiency on a 28 GHz patch antenna. The only
method in the comparison combining surrogate acceleration, uncertainty quantification, and
fabrication constraints. Converged on a quad-core CPU with no GPU, using curriculum learning
(32 → 64 → 128 step episodes) with VecNormalize.

`PyTorch` · `Stable-Baselines3` · `LightGBM` · `Optuna` · `CST API`

---

<details>
<summary><b>More projects</b></summary>

<br>

| Project | What it is |
|---|---|
| [**ai_data_scientist**](https://github.com/DNSdecoded/ai_data_scientist) | Seven sequential CrewAI agents take a raw dataset to cleaned data, trained models, charts, and an executive report. Every agent is bound to deterministic pandas/scikit-learn/SciPy tools, so the LLM orchestrates while the tools compute — reproducible and cheap on tokens. SQLite experiment store, LiteLLM provider abstraction, exponential-backoff retry on HTTP 429. |
| [**CipherChat**](https://github.com/DNSdecoded/CipherChat) | End-to-end encrypted messenger implementing the **Signal Protocol** — X3DH key agreement and Double Ratchet — with AES-256-GCM, TLS transport, perfect forward secrecy, TOFU key verification, and IPv4/IPv6 support. |
| [**landuse-cnn-eurosat**](https://github.com/DNSdecoded/landuse-cnn-eurosat) | Custom 3-layer CNN trained from scratch in PyTorch: 89% test accuracy on 27,000 EuroSAT images across 10 classes (70/15/15 split), with Grad-CAM hooks on the final Conv2d layer verifying the model learns spatial rather than texture features. |
| [**ResolverLab**](https://github.com/DNSdecoded/ResolverLab) | DNS benchmarking across 50+ filtered providers — block accuracy, latency, cache behavior — over UDP, TCP, DoH, and DoT, with automated HTML reporting. |

</details>

---

## Research

**Publications**

- *Bandwidth Enhancement of Slotted Hexagonal Patch Antenna for 6G Ultra-Fast Data Transfer and Brain-Computer Interface* — ICMOCE 2025, IIT Bhubaneswar. [DOI: 10.1109/ICMOCE64100.2025.11076991](https://doi.org/10.1109/ICMOCE64100.2025.11076991)
- *Bandwidth Optimization of Slotted Circular Patch Antenna for 6G Ultra-Fast Data Transfer and Brain-Computer Interface Application* — 16th ICCCNT 2025, IIT Indore. IEEE Xplore publication pending.
- *Uncertainty-Aware Reinforcement Learning System with Blended Surrogate Models for Electromagnetic Structure Optimization* — Accepted, WAMS 2026, BVRIT Hyderabad.

**Patent**

- *Design of Hexagonal Patch Antenna at 28 GHz* — Indian patent application No. 202541014595 A, published March 2025.

---

## Skills

**Languages** Python · SQL
**ML / RL** PyTorch · TensorFlow · scikit-learn · LightGBM · Stable-Baselines3 · Optuna · OpenCV
**NLP & GenAI** HuggingFace Transformers · LangChain · LangGraph · CrewAI · RAG · agentic and multi-agent systems · LLM evaluation & observability · fine-tuning · prompt engineering · multilingual embeddings · OCR
**MLOps & Backend** FastAPI · SQLAlchemy 2.0 · Docker · CI/CD · PostgreSQL · pgvector · ChromaDB · FAISS · Redis · MLflow · Prometheus · Vertex AI · GCP · Git · Linux
**Data** pandas · NumPy · SciPy · Matplotlib · Streamlit

---

## Training

| Program | Provider | Period |
|---|---|---|
| Generative AI | SkillHive Connect | Aug 2025 – Dec 2025 |
| AI/ML | Google for Developers | Jan 2025 – Mar 2025 |
| Cybersecurity | Palo Alto Networks | Oct 2024 – Dec 2024 |
| Data Science (RapidMiner) | Altair | Apr 2024 – Jun 2024 |

---

<div align="center">

[![GitHub stats](https://github-readme-stats.vercel.app/api?username=DNSdecoded&show_icons=true&hide_border=true&count_private=true&include_all_commits=true)](https://github.com/DNSdecoded)

**Open to entry-level AI/ML and software engineering roles.**
[Email](mailto:sanjaysakhinala@gmail.com) · [LinkedIn](https://linkedin.com/in/sanjaysakhinala) · [Portfolio](https://sanjaysakhinala.pages.dev)

</div>
