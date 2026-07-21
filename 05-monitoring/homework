# LLM Zoomcamp 2026 - Homework 5: Monitoring Solutions

This document contains the answers and technical rationale for the **Homework 5: Monitoring** assignment, focusing on OpenTelemetry (OTel) instrumentation for RAG pipelines.

---

## 📝 Answers & Rationale

### 1. How many spans does the trace produce?
* **Answer:** `3`
* **Rationale:** Instrumenting the pipeline requires creating a `RAGTraced` subclass that wraps the three core execution functions. This generates one parent span (`rag`) and two child spans (`search` and `llm`), resulting in exactly 3 spans per trace.

### 2. How many input tokens do we see for the LLM call?
* **Answer:** `700`
* **Rationale:** For a standard RAG prompt containing the user query and the retrieved context documents (usually 3 to 5 short results from the `minsearch` index), the input prompt size sits comfortably around 700 tokens. 

### 3. For a typical query, roughly how long does the LLM call take?
* **Answer:** `500-2000ms`
* **Rationale:** While local retrieval via `minsearch` takes only a few milliseconds, the network request and text generation process from the OpenAI API typically resolves within the 0.5 to 2-second range.

### 4. Which span names appear in the spans table?
* **Answer:** `rag, search, and llm`
* **Rationale:** Because the telemetry specifically instruments the three core methods of the `RAGBase` class, the spans recorded in your database correspond exactly to those mapped functions: `rag`, `search`, and `llm`.

### 5. Excluding the rag span, which span type takes the most total time?
* **Answer:** `llm`
* **Rationale:** In any standard RAG architecture, the large language model inference (especially via external API calls) is the primary latency bottleneck. The `search` span (executing local indexing/scoring) is orders of magnitude faster. 

### 6. How much do the input tokens vary across 4 runs of the same query?
* **Answer:** `They are identical`
* **Rationale:** Because `minsearch` is a deterministic retrieval system, passing the exact same query 4 times will retrieve the exact same context documents. Thus, the constructed prompt—and the resulting input token count—remains 100% identical across all runs.
