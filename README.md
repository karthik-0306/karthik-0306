# Hi, I'm Sai Karthik Thota

🎓 Final-year **B.Tech CSE** student at **Indian Institute of Information Technology, Kottayam**.  
🎯 Interested in **AI/ML engineering, research, data science**, and **systems-focused software engineering**.  
🔧 Open-source contributor to **PyTorch**, **Microsoft Agent Framework**, and **Google ADK Go**.

---

### Projects

#### [![PrismAI](https://img.shields.io/badge/PrismAI-8B5CF6?style=for-the-badge)](https://github.com/karthik-0306/PrismAI)

*Multi-Agent LLM Orchestration Platform*

A FastAPI orchestration engine that classifies and splits queries into **9 domains**, dispatches sub-queries in parallel, applies severity-gated (**0–3**) judgment with resplit-and-retry, and synthesizes answers through **LiteLLM** fallback chains. A query rewriter compresses verbose prompts (validated at **0.80** cosine similarity) for a **16.92% average token reduction** on LMSYS-Chat-1M, and conversation memory is summarized at 60% of the context window. Subagents cover DSA (**CoT output**), web search (**Tavily**), and a **3-judge EvaluatorSubagent** for response scoring.

![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![LiteLLM](https://img.shields.io/badge/-LiteLLM-111111?style=flat-square) ![React](https://img.shields.io/badge/-React-20232A?style=flat-square&logo=react&logoColor=61DAFB)

[Repository](https://github.com/karthik-0306/PrismAI) · [Live Demo](https://prism-ai-rust.vercel.app/)

#### [![ContextClosest](https://img.shields.io/badge/ContextClosest-0EA5E9?style=for-the-badge)](https://github.com/karthik-0306/ContextClosest)

*Hybrid Multimodal Product Search Engine*

A search engine for large product catalogs that cleans **147K** raw Amazon Berkeley Objects (ABO) listings into **56K** indexed products and fuses **LoRA-fine-tuned SigLIP 2** dense embeddings (**768-dim**, trained with **PEFT**) with **SPLADE** sparse vectors via **Reciprocal Rank Fusion (RRF)**. Vectors are indexed in **Qdrant Cloud**, product images and metadata are offloaded to **AWS S3**, and a **FastAPI** backend serves queries serverlessly on **Modal**.

![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![SigLIP 2](https://img.shields.io/badge/-SigLIP_2-8B5CF6?style=flat-square) ![Qdrant](https://img.shields.io/badge/-Qdrant-DC244C?style=flat-square) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Modal](https://img.shields.io/badge/-Modal-111111?style=flat-square)

[Repository](https://github.com/karthik-0306/ContextClosest) · [Live Demo](https://karthik-0306--contextclosest-search-web.modal.run/)

#### [![Volatility Forecasting](https://img.shields.io/badge/Volatility_Forecasting-10B981?style=for-the-badge)](https://github.com/karthik-0306/Volatility-Forecasting-in-Global-Financial-Markets-Using-TimeMixer)

*Volatility Forecasting in Global Assets (TimeMixer)*

Engineered a **TimeMixer** architecture forecasting multi-scale volatility across **4 asset classes** (Equities, ETFs, Crypto, Forex) and **5 temporal horizons**, computing **Yang-Zhang** estimators directly from live OHLCV data sourced from Yahoo Finance. Benchmarked against traditional **GARCH(1,1)** models, achieving a **35% reduction** in MAE and **39% improvement** in sMAPE across all horizons (**12, 96, 192, 336, 720 days**), and deployed as a live service via a **FastAPI** backend.

![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) ![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)

[Repository](https://github.com/karthik-0306/Volatility-Forecasting-in-Global-Financial-Markets-Using-TimeMixer) · [Live Demo](https://global-asset-volatility-forecasting.onrender.com/)

---

### Open Source Contributions

#### [![pytorch/pytorch](https://img.shields.io/badge/pytorch%2Fpytorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://github.com/pytorch/pytorch) [![Stars](https://img.shields.io/github/stars/pytorch/pytorch?style=for-the-badge&color=F59E0B)](https://github.com/pytorch/pytorch/stargazers) ![Contributions](https://img.shields.io/badge/contributions-2-0EA5E9?style=for-the-badge)

- **[#173989](https://github.com/pytorch/pytorch/pull/173989)** — Mixed-Precision NaN Propagation Guard ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #173885](https://github.com/pytorch/pytorch/issues/173885)

  FP16/BF16 training causes numbers to overflow to infinity, where (∞ − ∞) subtractions produce NaNs that silently corrupt model outputs. Root-caused this bug in PyTorch (`torch.compile`) and shipped a **CPU/GPU numerical guard** that forces the difference to zero instead of NaN, preventing catastrophic model corruption during large-scale training.

  > Independently adopted by **Amazon's AWS** PyTorch team into their production infrastructure ([commit a5d7261](https://github.com/amazon-contributing/upstream-to-pytorch/commit/a5d7261)).

- **[#185355](https://github.com/pytorch/pytorch/pull/185355)** — Pipeline Parallelism Hook Accumulation Fix ![Under Review](https://img.shields.io/badge/-Under_Review-D29922?style=flat-square) · [Issue #185331](https://github.com/pytorch/pytorch/issues/185331)

  `torch.distributed.pipelining` reused memory buffers during LLM training, causing hooks to accumulate, leak memory, and corrupt gradients. Root-caused and fixed via isolated independent tensors, restoring stable parallel execution.

#### [![microsoft/agent-framework](https://img.shields.io/badge/microsoft%2Fagent--framework-0078D4?style=for-the-badge)](https://github.com/microsoft/agent-framework) [![Stars](https://img.shields.io/github/stars/microsoft/agent-framework?style=for-the-badge&color=F59E0B)](https://github.com/microsoft/agent-framework/stargazers) ![Contributions](https://img.shields.io/badge/contributions-4-0EA5E9?style=for-the-badge)

- **[#7772](https://github.com/microsoft/agent-framework/pull/7772)** — Agent Tool-Loop `max_duration_seconds` Wall-Clock Bound ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #7587](https://github.com/microsoft/agent-framework/issues/7587)

  Added a configurable `max_duration_seconds` bound to the tool-calling loop, previously capped only by iteration and call count. Implemented graceful degradation on timeout, with duration tracked cumulatively across human-approval round-trips.

- **[#6052](https://github.com/microsoft/agent-framework/pull/6052)** — AWS Bedrock Structured Output Enablement ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #5966](https://github.com/microsoft/agent-framework/issues/5966)

  Enabled native AWS Bedrock structured outputs within MAF by implementing the schema translation layer. Devised a precise wire-format resolving community serialization bugs, delivering recursive schema enforcement and multi-shape input handling.

- **[#7283](https://github.com/microsoft/agent-framework/pull/7283)** — FoundryAgent `OPENAI_CHAT_MODEL` Inheritance Fix ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #7272](https://github.com/microsoft/agent-framework/issues/7272)

  Debugged FoundryAgent's inherited `OPENAI_CHAT_MODEL` leak causing valid agent-reference requests to fail against the Foundry backend. Developed a two-layer fix combining source-level isolation with defense-in-depth stripping.

- **[#5947](https://github.com/microsoft/agent-framework/pull/5947)** — MCP Progressive Tool Discovery ![Superseded](https://img.shields.io/badge/-Superseded-6E7781?style=flat-square) by [#6233](https://github.com/microsoft/agent-framework/pull/6233) ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #5821](https://github.com/microsoft/agent-framework/issues/5821)

  Implemented `as_progressive_tools()` on `MCPTool`, enabling progressive tool discovery to reduce context token overhead for large MCP servers exposing 50–200+ tools. Superseded by a MAF member ([#6233](https://github.com/microsoft/agent-framework/pull/6233)) for broader implementation than MCP.

#### [![google/adk-go](https://img.shields.io/badge/google%2Fadk--go-00ADD8?style=for-the-badge&logo=go&logoColor=white)](https://github.com/google/adk-go) [![Stars](https://img.shields.io/github/stars/google/adk-go?style=for-the-badge&color=F59E0B)](https://github.com/google/adk-go/stargazers) ![Contributions](https://img.shields.io/badge/contributions-1-0EA5E9?style=for-the-badge)

- **[#1729](https://github.com/google/adk-go/pull/1729)** — Vertex AI Session Memory: Code Execution and File Data Serialization ![Merged](https://img.shields.io/badge/-Merged-2EA043?style=flat-square) · [Issue #1728](https://github.com/google/adk-go/issues/1728)

  `adk-go` silently dropped `ExecutableCode`, `CodeExecutionResult`, and `FileData` when converting to the Vertex AI Protobuf format, so code-execution agents lost the code they ran and hallucinated on the next turn. Root-caused the loss to two mapping functions in `session/vertexai` and implemented the missing **round-trip serialization**, backed by table-driven tests refactored to `cmp.Diff` at a maintainer's request.

---

### Contact

[![Email](https://img.shields.io/badge/-Email-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:karthikthota7777@gmail.com) [![LinkedIn](https://img.shields.io/badge/-LinkedIn-0A66C2?style=flat-square)](https://www.linkedin.com/in/karthikthota29/)
