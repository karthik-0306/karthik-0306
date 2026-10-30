<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=200&color=0:0EA5E9,50:8B5CF6,100:EE4C2C&text=Sai%20Karthik%20Thota&fontColor=ffffff&fontSize=48&fontAlignY=38&desc=I%20fix%20bugs%20and%20build%20features%20inside%20the%20tools%20AI%20engineers%20use&descSize=16&descAlignY=60" alt="Karthik Thota" />

<div align="center">

Final-year **B.Tech CSE** at **Indian Institute of Information Technology, Kottayam**

🎯 AI/ML Engineering · Research · Data Science · Software Engineering

![Google](https://img.shields.io/badge/Google_ADK_Go-4285F4?style=for-the-badge&logo=google&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Apache](https://img.shields.io/badge/Apache_SeaTunnel-D22128?style=for-the-badge&logo=apache&logoColor=white)
![Microsoft](https://img.shields.io/badge/Microsoft_Agent_Framework-0078D4?style=for-the-badge)

[![Email](https://img.shields.io/badge/-Email-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:karthikthota7777@gmail.com) [![LinkedIn](https://img.shields.io/badge/-LinkedIn-0A66C2?style=flat-square)](https://www.linkedin.com/in/karthikthota29/)

</div>

---

## 🔥 Currently working on

<table>
<tr>
<td width="33%" valign="top">

![Google](https://img.shields.io/badge/Google_ADK_Go-4285F4?style=flat-square&logo=google&logoColor=white)

### Gemini context caching
Issue [#1937](https://github.com/google/adk-go/issues/1937) · PR [#1951](https://github.com/google/adk-go/pull/1951)

🟡 **Under Review**

</td>
<td width="33%" valign="top">

![Apache](https://img.shields.io/badge/Apache_SeaTunnel-D22128?style=flat-square&logo=apache&logoColor=white)

### pip install launcher
Issue [#12707](https://github.com/apache/seatunnel/issues/12707) · PRs [#12740](https://github.com/apache/seatunnel/pull/12740) [#12857](https://github.com/apache/seatunnel/pull/12857) [#12994](https://github.com/apache/seatunnel/pull/12994) [#12858](https://github.com/apache/seatunnel/pull/12858)

🟡 **In Progress**

</td>
<td width="33%" valign="top">

![Microsoft](https://img.shields.io/badge/Microsoft_Agent_Framework-0078D4?style=flat-square)

### Tasks lost across servers
Issue [#8760](https://github.com/microsoft/agent-framework/issues/8760) · PR [#9387](https://github.com/microsoft/agent-framework/pull/9387)

🟡 **Phase 1 Under Review**

</td>
</tr>
</table>

---

## Google ADK Go

![Google](https://img.shields.io/badge/Google-ADK_Go-4285F4?style=for-the-badge&logo=google&logoColor=white)

### Gemini context caching &nbsp; 🟡 **Under Review**
**Issue [#1937](https://github.com/google/adk-go/issues/1937) · PR [#1951](https://github.com/google/adk-go/pull/1951)**

Added Gemini context caching as an ADK Go feature. Gemini API calls store repeated prompt prefixes (instructions, tools, history) once and reuse them across turns, cutting input tokens. Built invalidation and cleanup, persisted in SQL sessions.

**In plain terms:** every turn of a chat normally re-sends the same long prefix (the agent's instructions, its tool definitions and the earlier conversation), and you are billed for those input tokens every time.

- **Turn 1:** the agent sends the full prompt, as usual.
- **Turn 2:** once the same prefix has repeated, it is stored on Gemini's servers as a cache. The request now says "use cache X" and only sends the new message, so the repeated part isn't billed again at full price.
- **Keeping it correct:** if the instructions or history change, the old cache is invalidated and replaced. Old caches are deleted after the reply reaches the user, and the cache's reference is saved with the session in SQL, so it survives restarts.

It is opt-in, so existing agents are unaffected.

### Shipped and in review

| Status | PR | What was wrong, and what I did | Issue |
|---|---|---|---|
| 🟢 **Merged** | **[#1729](https://github.com/google/adk-go/pull/1729)** | **Vertex AI memory silently dropped code-execution and file data**, so agents forgot the code they had run and made things up on the next turn. Added the missing round-trip serialization. | [#1728](https://github.com/google/adk-go/issues/1728) |
| 🟢 **Merged** | **[#1748](https://github.com/google/adk-go/pull/1748)** | **Optional prompt placeholders like `{user_data?}` swallowed every error**, even a dead database, and the agent carried on with a broken prompt. Now only a genuine "not found" is ignored. | [#1747](https://github.com/google/adk-go/issues/1747) |
| 🟡 **Under Review** | **[#1730](https://github.com/google/adk-go/pull/1730)** | **The agent graph skipped toolset tools and sub-agent links.** It now resolves toolsets (with a timeout so a hung server can't stall it) and draws the missing connections. | [#1726](https://github.com/google/adk-go/issues/1726) |

---

## PyTorch

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)

| Status | PR | What was wrong, and what I did | Issue |
|---|---|---|---|
| 🟢 **Merged** | **[#173989](https://github.com/pytorch/pytorch/pull/173989)** | **Mixed-precision NaN guard.** FP16/BF16 training can overflow to infinity, and `∞ − ∞` silently produces NaNs that corrupt a model. Root-caused it in `torch.compile` and shipped a CPU/GPU guard that forces the difference to zero. Independently adopted by **Amazon's AWS** PyTorch team in production ([commit a5d7261](https://github.com/amazon-contributing/upstream-to-pytorch/commit/a5d7261)). | [#173885](https://github.com/pytorch/pytorch/issues/173885) |
| 🟡 **Under Review** | **[#185355](https://github.com/pytorch/pytorch/pull/185355)** | **Pipeline parallelism hook accumulation.** `torch.distributed.pipelining` reused memory buffers during LLM training, so hooks piled up, leaked memory and corrupted gradients. Fixed with isolated, independent tensors. | [#185331](https://github.com/pytorch/pytorch/issues/185331) |

---

## Apache SeaTunnel

![Apache](https://img.shields.io/badge/Apache-SeaTunnel-D22128?style=for-the-badge&logo=apache&logoColor=white)

### A pip install launcher for SeaTunnel &nbsp; 🟡 **In Progress**
**Issue [#12707](https://github.com/apache/seatunnel/issues/12707)** · co-developing

**The problem.** To try SeaTunnel today you download a **~470 MB** package, unpack it, set environment variables, make sure Java is installed and add connectors by hand. That is a lot of setup before a first run, especially in notebooks and CI.

**The goal:** `pip install` and go. A small Python package that fetches and verifies the official engine on first run, then launches it. I'm building it as small, reviewable steps:

| Step | PR | What it does |
|---|---|---|
| 1 | [#12740](https://github.com/apache/seatunnel/pull/12740) · 🟢 **Merged** | **Fail-fast JDK check:** finds Java, checks the version and gives a clear fix-it message instead of a cryptic JVM crash |
| 2 | [#12857](https://github.com/apache/seatunnel/pull/12857) · 🟢 **Merged** | **SDK CI:** the Python SDK now builds and checks itself automatically on every PR |
| 2b | [#12994](https://github.com/apache/seatunnel/pull/12994) · 🟢 **Merged** | **CI follow-up:** pinned the workflow to ubuntu-24.04 so Python 3.9 installs reliably |
| 3 | [#12858](https://github.com/apache/seatunnel/pull/12858) · 🔵 **Approved** | **Plugin installer:** enables only the connectors you ask for, with atomic writes and a byte-exact rollback if anything fails |

### Shipped

| Status | PR | What was wrong, and what I did | Issue |
|---|---|---|---|
| 🟢 **Merged** | **[#12573](https://github.com/apache/seatunnel/pull/12573)** | **The Paimon connector accepted blank warehouse, database and table values** and only failed later at runtime. Added declarative `notBlank` validation so bad config is rejected when the job is submitted. | [#11007](https://github.com/apache/seatunnel/issues/11007) |

---

## Microsoft Agent Framework

![Microsoft](https://img.shields.io/badge/Microsoft-Agent_Framework-0078D4?style=for-the-badge)

### Background tasks that go missing across servers &nbsp; 🟡 **In Progress**
**Issue [#8760](https://github.com/microsoft/agent-framework/issues/8760)**: the background-task provider cannot tell a task running on *another server* from one whose owner *died*.

**The problem.** An agent can start a background task ("research this while we keep chatting"). The task has two halves: a **saved record** (status, result) that travels with the conversation, and the **live work**, which exists only in the memory of the one server that started it. When the next message lands on a *different* server, that server sees "marked running, but I can't find it" and declares the task **LOST**. It can't tell "the server crashed" from "it's just running somewhere else". The result:

- **Duplicate work:** the model restarts a "lost" task while the original is still running, so you pay twice and two writers can touch the same files
- **Lost results:** when the original finishes, nobody records its answer
- **Zombie tasks:** deleting a conversation on one server doesn't stop its tasks on another

I'm fixing this in two phases.

**Phase 1: PR [#9387](https://github.com/microsoft/agent-framework/pull/9387)** · 🟡 **Under Review**
A finished task was deleted from memory the instant it completed, so restoring a session snapshot taken *while it was running* could not find it and threw the result away. My PR keeps finished tasks until they are cleared, tags every run with an execution ID so a stale snapshot can never pick up another run's result, and makes `release_session(timeout=...)` return on time even if a task ignores cancellation.

**Phase 2:** once Phase 1 is merged, I'll submit an **ADR** (architecture decision record) for the real cross-server design and start implementing as soon as the Microsoft team accepts it.

![Microsoft Agent Framework](https://img.shields.io/badge/Microsoft_Agent_Framework-0078D4?style=flat-square) ![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) ![ADR](https://img.shields.io/badge/-ADR-6E7781?style=flat-square)

### Shipped

| Status | PR | What was wrong, and what I did | Issue |
|---|---|---|---|
| 🟢 **Merged** | **[#8774](https://github.com/microsoft/agent-framework/pull/8774)** | **Errors in streaming hooks vanished silently.** If a hook or mapper crashed mid-stream, the stream never recorded the error, so monitoring spans closed looking healthy. I moved that code inside the stream's error handling. | [#8765](https://github.com/microsoft/agent-framework/issues/8765) |
| 🟢 **Merged** | **[#7772](https://github.com/microsoft/agent-framework/pull/7772)** | **An agent's tool loop could run for too long** (it was only capped by call count). Added a `max_duration_seconds` time limit that stops gracefully and keeps counting across human-approval pauses. | [#7587](https://github.com/microsoft/agent-framework/issues/7587) |
| 🟢 **Merged** | **[#6052](https://github.com/microsoft/agent-framework/pull/6052)** | **AWS Bedrock couldn't return structured output.** Built the schema translation layer and a precise wire format, with nested schemas and multiple input shapes. | [#5966](https://github.com/microsoft/agent-framework/issues/5966) |
| 🟢 **Merged** | **[#7283](https://github.com/microsoft/agent-framework/pull/7283)** | **FoundryAgent inherited a stray `OPENAI_CHAT_MODEL`** that broke valid requests. Fixed at the source and stripped defensively as a second layer. | [#7272](https://github.com/microsoft/agent-framework/issues/7272) |
| ⚪ **Superseded** | **[#5947](https://github.com/microsoft/agent-framework/pull/5947)** | **MCP servers with 50–200+ tools flood the model's context.** Added `as_progressive_tools()` to discover tools progressively. A maintainer shipped a broader version in [#6233](https://github.com/microsoft/agent-framework/pull/6233) (🟢 **Merged**). | [#5821](https://github.com/microsoft/agent-framework/issues/5821) |

---

## 🚀 Projects

### [PrismAI](https://github.com/karthik-0306/PrismAI): multi-agent LLM orchestration platform
No single LLM is best at everything, so PrismAI acts as a router. A FastAPI engine classifies each query into **9 domains**, splits it into sub-queries, sends them in parallel to the best model, **judges** every answer on a 0–3 severity scale (re-splitting and retrying bad ones) and merges the results through **LiteLLM** fallback chains across Groq and Gemini.

- **Query rewriter:** compresses verbose prompts, accepted only if the meaning stays above **0.80** cosine similarity. **16.92%** average token reduction on LMSYS-Chat-1M.
- **Conversation memory:** once a chat uses 60% of the model's context window, older messages are folded into a rolling summary and the latest turns stay verbatim.
- **Subagents:** DSA solver with step-by-step (CoT) output, Tavily web search with cited sources, and a **3-judge EvaluatorSubagent** scoring answers on 7 metrics.

![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![LiteLLM](https://img.shields.io/badge/-LiteLLM-111111?style=flat-square) ![React](https://img.shields.io/badge/-React-20232A?style=flat-square&logo=react&logoColor=61DAFB)

[Repository](https://github.com/karthik-0306/PrismAI) · [Live Demo](https://prism-ai-rust.vercel.app/)

### [ContextClosest](https://github.com/karthik-0306/ContextClosest): hybrid multimodal product search
Cleans **147K** raw Amazon Berkeley Objects listings into **56K** indexed products and fuses **LoRA-fine-tuned SigLIP 2** image/text embeddings (768-dim, trained with PEFT) with **SPLADE** sparse vectors using **Reciprocal Rank Fusion**. Vectors live in **Qdrant Cloud**, images and metadata on **AWS S3**, and a **FastAPI** backend serves queries serverlessly on **Modal**.

![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![SigLIP 2](https://img.shields.io/badge/-SigLIP_2-8B5CF6?style=flat-square) ![Qdrant](https://img.shields.io/badge/-Qdrant-DC244C?style=flat-square) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Modal](https://img.shields.io/badge/-Modal-111111?style=flat-square)

[Repository](https://github.com/karthik-0306/ContextClosest) · [Live Demo](https://karthik-0306--contextclosest-search-web.modal.run/)

### [Volatility Forecasting with TimeMixer](https://github.com/karthik-0306/Volatility-Forecasting-in-Global-Financial-Markets-Using-TimeMixer)
A **TimeMixer** model forecasting volatility across **4 asset classes** (equities, ETFs, crypto, forex) and **5 horizons** (12 to 720 days), computed with **Yang-Zhang** estimators from live Yahoo Finance data. Against **GARCH(1,1)** it cuts MAE by **35%** and improves sMAPE by **39%**. Deployed as a live **FastAPI** service.

![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) ![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)

[Repository](https://github.com/karthik-0306/Volatility-Forecasting-in-Global-Financial-Markets-Using-TimeMixer) · [Live Demo](https://global-asset-volatility-forecasting.onrender.com/)

---

<div align="center">

### 📬 Contact

[![Email](https://img.shields.io/badge/-Email-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:karthikthota7777@gmail.com) [![LinkedIn](https://img.shields.io/badge/-LinkedIn-0A66C2?style=flat-square)](https://www.linkedin.com/in/karthikthota29/)

</div>
