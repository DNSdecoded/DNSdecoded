<div align="center">

# Sanjay Sakhinala

### AI/ML Engineer — Agentic RAG · LLM Evaluation · Reinforcement Learning

[![Portfolio](https://img.shields.io/badge/Portfolio-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://sanjaysakhinala.pages.dev)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/sanjaysakhinala)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sanjaysakhinala@gmail.com)
[![Resume](https://img.shields.io/badge/Resume-2E7D32?style=for-the-badge&logo=readthedocs&logoColor=white)](https://sanjaysakhinala.pages.dev/SanjayBhargav_Resume.pdf)

Hyderabad, India · Open to entry-level AI/ML and software engineering roles

</div>

---

## About

AI/ML engineer working on retrieval-augmented generation, agentic systems, LLM evaluation, and reinforcement learning. B.Tech in Electronics and Communication Engineering, 2025.

The thread running through everything below is **making LLM output verifiable** — citation grounding enforced at the schema level, NLI-based claim-level faithfulness checks, and offline eval harnesses that turn "the answer looks right" into a number you can regress against. Author of 3 IEEE publications and 1 Indian patent.

Currently extending IndicRAG's evaluation harness and pushing AgentOps toward a drop-in tracing SDK for third-party agent stacks.

**Languages** Python · SQL
**ML / RL** PyTorch · TensorFlow · scikit-learn · LightGBM · Stable-Baselines3 · Optuna · OpenCV
**NLP / LLM** HuggingFace Transformers · LangChain · LangGraph · CrewAI · BGE-M3 · Gemini
**Backend / Infra** FastAPI · SQLAlchemy 2.0 · PostgreSQL · pgvector · ChromaDB · FAISS · Redis · Docker · Nginx · Prometheus · MLflow · GCP / Vertex AI · Git · Linux
**Data** pandas · NumPy · SciPy · Matplotlib · Streamlit

---

## Featured Work

### 🔷 [IndicRAG](https://github.com/DNSdecoded/IndicRAG) — Multilingual Agentic RAG

[![Commits](https://img.shields.io/github/commit-activity/t/DNSdecoded/IndicRAG?style=flat-square&label=commits)](https://github.com/DNSdecoded/IndicRAG/commits)
[![Last commit](https://img.shields.io/github/last-commit/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/commits)
[![License](https://img.shields.io/github/license/DNSdecoded/IndicRAG?style=flat-square)](https://github.com/DNSdecoded/IndicRAG/blob/main/LICENSE)

| | |
|---|---|
| **Problem** | RAG systems answer confidently in English and fail quietly in Indic languages, with no signal for when a citation doesn't actually support the claim. |
| **Approach** | LangGraph `StateGraph` — planner → tool selector → executor → generator → reflexion evaluator — with 6 tools and dual-gate verification (`bge-reranker-v2-m3` faithfulness + Gemini completeness, threshold 0.75). Hybrid BGE-M3 dense + BM25 retrieval fused with RRF (k=60), then cross-encoder and ColBERT MaxSim reranking, then NLI claim-level faithfulness verification. |
| **Result** | Precision@5 **1.000**, Recall@5 **0.917**, MRR **1.000**, Citation Grounding **0.938** on manually labeled relevance judgments, across 10 Indian languages and English. Reflexion loops converge within 3 iterations under a 45 s wall-clock budget. |
| **Stack** | `LangGraph` `BAAI/bge-m3` `ChromaDB` `Gemini` `FastAPI` `PyMuPDF` `Prometheus` `Nginx` `Docker Compose` |

Solo-developed continuously since November 2025 — 100+ commits through `v2.4.0`, PR-based review workflow, semantic versioning, documented rollback procedures. The hardest problem wasn't retrieval quality but *knowing* retrieval quality: multilingual relevance judgments had to be hand-labeled before any of the numbers above meant anything. Building the reflexion loop taught me that a self-correcting agent without a hard iteration and wall-clock budget will happily spend unbounded tokens convincing itself.

---

### 🔷 [Meridian UM](https://github.com/DNSdecoded/meridian-um-platform) — AI-Augmented Prior Authorization

| | |
|---|---|
| **Problem** | In regulated review workflows, an ungrounded model finding is worse than no finding — and prompt changes are usually evaluated anecdotally. |
| **Approach** | Citation grounding enforced at the **schema level** (findings must resolve to a document span or policy-clause ID; uncited findings rejected, low-confidence routed to review) plus a PostgreSQL `CHECK` constraint blocking any denial lacking a recorded human attestation. 11-state forward-only case workflow: step-skipping rejected, repeats idempotent. |
| **Result** | A property test fails if either invariant is weakened. Offline eval harness reports accuracy, per-label P/R/F1, and citation validity over ~150 labeled synthetic cases. |
| **Stack** | `FastAPI (async)` `SQLAlchemy 2.0` `PostgreSQL 16` `pgvector` `OCR` `JWT` `Apache-2.0` |

> **Synthetic data only.** No real patient data anywhere in this project.

---

### 🔷 [AgentOps](https://github.com/DNSdecoded/AgentOps) — LLM Agent Observability & Evaluation

| | |
|---|---|
| **Problem** | Agent quality regressions are invisible without per-run traces and per-run metrics — you find out from users, not from CI. |
| **Approach** | Async FastAPI + PostgreSQL over a 12-table trace schema exposed via REST and WebSocket, plus a Python tracing SDK that buffers steps client-side and captures exceptions as failed runs, so instrumentation never crashes the host application. |
| **Result** | Per-run faithfulness, retrieval relevance, hallucination score, and unsupported-claim extraction, via a dual-path evaluation engine — zero-cost token-overlap heuristics by default, swappable to a Gemini LLM judge. Prompt Lab A/B-tests versions on success rate, cost, latency, and hallucination delta. |
| **Stack** | `FastAPI` `PostgreSQL` `Next.js 14` `React Flow` `Python SDK` `Docker Compose` |

---

### 🔷 [RL for Antenna Design Optimization](https://sanjaysakhinala.pages.dev/blog/rl-antenna-design.html) — Accepted, WAMS 2026

| | |
|---|---|
| **Problem** | Each CST Studio evaluation is expensive; a genetic-algorithm baseline needed ~1,500 of them to converge on a 28 GHz patch antenna. |
| **Approach** | Soft Actor-Critic trained over 2.68M steps against a blended surrogate ensemble (2×LightGBM + MLP + RidgeCV, <5 ms inference) with uncertainty-aware reward shaping and an active-learning loop that re-simulates top candidates to limit model drift. |
| **Result** | **420 simulations — a 72% reduction.** Outperformed GA, PSO, DQN, PPO, and DDPG: −52.2 dB return loss, 8.93% FBW, 5.272 dBi gain, 80.6% radiation efficiency. Converged on a quad-core CPU with no GPU, using curriculum learning (32 → 64 → 128 step episodes) with `VecNormalize`. |
| **Stack** | `PyTorch` `Stable-Baselines3` `LightGBM` `Optuna` `CST Studio API` |

---

<details>
<summary><b>More projects</b></summary>

<br>

| Project | What it is |
|---|---|
| [**ai_data_scientist**](https://github.com/DNSdecoded/ai_data_scientist) | Seven sequential CrewAI agents take a raw dataset to cleaned data, trained models, charts, and an executive report. Every agent is bound to deterministic pandas/scikit-learn/SciPy tools, so the LLM orchestrates while the tools compute. SQLite experiment store, LiteLLM provider abstraction, exponential-backoff retry on HTTP 429. |
| [**landuse-cnn-eurosat**](https://github.com/DNSdecoded/landuse-cnn-eurosat) | Custom 3-layer CNN trained from scratch in PyTorch — 89% test accuracy on 27,000 EuroSAT images across 10 classes, with Grad-CAM hooks on the final `Conv2d` layer verifying the model learns spatial rather than texture features. |
| [**CipherChat**](https://github.com/DNSdecoded/CipherChat) | End-to-end encrypted messenger implementing the Signal Protocol — X3DH key agreement and Double Ratchet — with AES-256-GCM, TLS transport, perfect forward secrecy, and TOFU key verification. |
| [**ResolverLab**](https://github.com/DNSdecoded/ResolverLab) | DNS benchmarking across 50+ filtered providers — block accuracy, latency, cache behavior — over UDP, TCP, DoH, and DoT, with automated HTML reporting. |

</details>

---

## Research

**Publications**

- *Uncertainty-Aware Reinforcement Learning System with Blended Surrogate Models for Electromagnetic Structure Optimization* — Accepted, WAMS 2026, BVRIT Hyderabad.
- *Bandwidth Enhancement of Slotted Hexagonal Patch Antenna for 6G Ultra-Fast Data Transfer and Brain-Computer Interface* — ICMOCE 2025, IIT Bhubaneswar. [DOI: 10.1109/ICMOCE64100.2025.11076991](https://doi.org/10.1109/ICMOCE64100.2025.11076991)
- *Bandwidth Optimization of Slotted Circular Patch Antenna for 6G Ultra-Fast Data Transfer and Brain-Computer Interface Application* — 16th ICCCNT 2025, IIT Indore. IEEE Xplore publication pending.

**Patent** — *Design of Hexagonal Patch Antenna at 28 GHz*, Indian patent application No. 202541014595 A, published March 2025.

---

## Training

**Programs** — Generative AI, SkillHive Connect (Aug–Dec 2025) · AI/ML, Google for Developers (Jan–Mar 2025) · Cybersecurity, Palo Alto Networks (2024) · Data Science, Altair (2024)
**Certificates** — Google Data Analytics · Google Cybersecurity · NPTEL Cloud Computing · Google Cloud skill badges (TensorFlow on GCP, Vertex AI Pipelines)

---

## Fun Facts

- 📡 I came to machine learning through antenna design — my first optimization problem was a physical object, not a dataset.
- 🔍 I use Grad-CAM to check whether a CNN is cheating, not to make pretty heatmaps. Texture shortcuts don't show up in an accuracy number.
- 🌐 The handle is `DNSdecoded`, and there's a resolver benchmark behind it: 50+ providers across UDP, TCP, DoH, and DoT.

---

<div align="center">

[GitHub](https://github.com/DNSdecoded) · [LinkedIn](https://linkedin.com/in/sanjaysakhinala) · [Portfolio](https://sanjaysakhinala.pages.dev) · [Email](mailto:sanjaysakhinala@gmail.com)

*"The purpose of computing is insight, not numbers."* — Richard Hamming

</div>
