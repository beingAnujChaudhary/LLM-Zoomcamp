# 🚀 Module 3 Homework: AI Orchestration with Kestra

Welcome to the solution repository for **Module 3: AI Orchestration** of the [LLM Zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp/) by DataTalksClub. 

This homework explores the practical applications of Kestra for orchestrating AI workflows, including context engineering, Retrieval-Augmented Generation (RAG), AI agents, and token optimization.

---

## 📋 Prerequisites

Before running the flows in this repository, ensure you have:
1. Completed the [Module 3 lessons](../../../03-orchestration/README.md).
2. Kestra running locally with API keys configured (including the Gemini API key for the AI Copilot).
3. Imported all flows from the `03-orchestration/flows/` directory.

---

## 💡 Homework Solutions

Below are the answers and detailed explanations for the homework questions.

### Question 1: Context Engineering
**Prompt Experiment:** "Create a Kestra flow that loads NYC taxi data from CSV to BigQuery"

**Question:** What is the primary reason AI Copilot generates better Kestra flows compared to a general LLM like ChatGPT?

**✅ Answer:** **AI Copilot has access to current Kestra plugin documentation**

**Explanation:** General LLMs rely on their pre-training data, which may be outdated or lack specific syntax for proprietary tools. Kestra's AI Copilot utilizes context engineering (via RAG) to inject up-to-date, official Kestra plugin documentation directly into the prompt, ensuring the generated YAML is accurate and syntactically correct.

---

### Question 2: RAG vs No RAG
**Experiment:** Run `1_chat_without_rag.yaml` and `2_chat_with_rag.yaml` and query them about Kestra 1.1 features.

**Question:** The non-RAG response about Kestra 1.1 features is best described as:

**✅ Answer:** **Vague, generic, or fabricated — the model guesses from training data**

**Explanation:** Without Retrieval-Augmented Generation (RAG), the LLM is forced to rely solely on its internal weights. If the specific release notes for Kestra 1.1 were not heavily represented in its training data, the model will hallucinate or provide generic answers. RAG solves this by fetching the exact, up-to-date release notes and grounding the model's response in factual context.

---

### Question 3: Token usage — short summary
**Experiment:** Run `4_simple_agent.yaml` with `summary_length = short`.

**Question:** What is the approximate **output** token count for `multilingual_agent`?

**✅ Answer:** **60-100 tokens**

**Explanation:** A "short" summary typically consists of 1-2 concise sentences. When processed and potentially translated by the agent, the output naturally falls into the 60-100 token range. (5-15 tokens is too brief for a meaningful summary, while 200+ tokens represents a much longer text).

---

### Question 4: Token usage — long summary
**Experiment:** Run `4_simple_agent.yaml` with `summary_length = long`.

**Question:** Roughly how many times more output tokens does the long summary use compared to the short summary?

**✅ Answer:** **2-5x more**

**Explanation:** A "long" summary expands the detail significantly, usually turning a 1-2 sentence overview into a multi-paragraph explanation. In LLM token generation, expanding from a short summary to a detailed long summary typically scales the output token count by a factor of 2 to 5.

---

### Question 5: Modifying a flow
**Experiment:** Modify the `english_brevity` task in `4_simple_agent.yaml` to ask for exactly **3 sentences** instead of 1. Run with `summary_length = long`.

**Question:** How does the `english_brevity` output token count compare to the original 1-sentence version?

**✅ Answer:** **2-4x more**

**Explanation:** Token count scales almost linearly with the length of the generated text. By explicitly constraining the model to generate 3 sentences instead of 1, the output length (and thus the token count) naturally increases by a factor of roughly 3, which falls perfectly into the 2-4x range.

---

### Question 6: Best Practices
**Question:** For production workflows requiring deterministic, repeatable results with strict compliance requirements (e.g., financial reporting), which approach is most appropriate?

**✅ Answer:** **Use traditional task-based workflows for predictability and auditability**

**Explanation:** While AI agents are powerful for dynamic, exploratory tasks, they introduce non-determinism (the LLM might choose different tools or paths on different runs). In highly regulated industries like finance, strict auditability and 100% predictable execution paths are mandatory. Traditional, explicitly defined task-based workflows guarantee that the exact same steps are executed in the exact same order every time.

```mermaid
flowchart TD
    A[Production Workflow<br/>Strict Compliance] --> B{What's Best?}
    
    B -->|❌ Wrong| C[Always use AI agents]
    B -->|❌ Wrong| D[Only RAG without agents]
    B -->|❌ Wrong| E[Only web search tools]
    B -->|✅ Correct| F[Traditional task-based workflows]
    
    F --> G[Predictable ✅]
    F --> H[Auditable ✅]
    F --> I[Repeatable ✅]
    
    style F fill:#c8e6c9,stroke:#2e7d32
    style G fill:#c8e6c9,stroke:#2e7d32
    style H fill:#c8e6c9,stroke:#2e7d32
    style I fill:#c8e6c9,stroke:#2e7d32
---

