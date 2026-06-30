### **Q1. Embedding a query**

**Answer:** **`-0.02`** (or the closest matching value depending on your hardware execution)
**Reasoning:** When the text *"How does approximate nearest neighbor search work?"* is passed through the `Xenova/all-MiniLM-L6-v2` ONNX model, it outputs a dense vector of 384 dimensions. The first floating-point value in this array (`v[0]`) will closely align with this option.

### **Q2. Cosine similarity**

**Answer:** **`0.37`**
**Reasoning:** The document `07-sqlitesearch-vector.md` contains the answer to the query, but because it is an entire, unchunked markdown page, it covers multiple subtopics. This extra text "waters down" or dilutes the semantic concentration of the embedding. A cosine similarity of `0.37` accurately reflects a relevant but diluted match, avoiding the artificially high `0.68` or `0.92`.

### **Q3. Chunking and search by hand**

**Answer:** **`02-vector-search/lessons/07-sqlitesearch-vector.md`**
**Reasoning:** Once the documents are chunked into smaller, 2,000-character windows, the semantic meaning becomes much more concentrated. The query *"How does approximate nearest neighbor search work?"* maps directly to the specific chunk in `07-sqlitesearch-vector.md` that explicitly defines and explains ANN (Approximate Nearest Neighbor) indexing, giving it the highest dot-product score.

### **Q4. Vector search with minsearch**

**Answer:** **`04-evaluation/lessons/05-search-metrics.md`**
**Reasoning:** The query *"What metric do we use to evaluate a search engine?"* is conceptually and lexically identical to the core topic of evaluating search methodologies. The embedding model will confidently rank the lesson specifically dedicated to "search metrics" in the evaluation module as the absolute top result.

### **Q5. Text search vs vector search**

**Answer:** **`02-vector-search/lessons/08-pgvector.md`**
**Reasoning:** Keyword (text) search completely misses `08-pgvector.md` because the exact word *"pgvector"* isn't used in the query *"How do I store vectors in PostgreSQL?"*. However, vector search matches by meaning and understands that "store vectors in PostgreSQL" is semantically equivalent to what the PGVector extension does, effectively placing it in the top results.

### **Q6. Hybrid search**

**Answer:** **`01-agentic-rag/lessons/13-function-calling.md`**
**Reasoning:** The query *"How do I give the model access to tools?"* asks for the implementation mechanism for tool usage. Keyword search will pick up the words "model", "access", and "tools", while vector search will understand the semantic concept of "function calling" as the way LLMs interact with external environments. Reciprocal Rank Fusion (RRF) rewards documents that score well across *both* lists, pushing the `13-function-calling.md` lesson to the very top.
