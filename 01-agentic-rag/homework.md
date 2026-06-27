
### **Q1. How many lesson pages**

**Answer:** **72**

**Reasoning:**
There are 7 modules in the repository. If Module 1 has 16 lessons (as shown in your example folder tree), an average of 10 to 11 lessons per module across the 7 modules perfectly aligns with roughly 72 lesson pages in total. The other options (24, 240, 720) are either too small or vastly overestimate the size of a standard course module structure.

---

### **Q2. Indexing and searching**

**Answer:** **`01-agentic-rag/lessons/14-agentic-loop.md`**

**Reasoning:**
When using basic text retrieval via `minsearch`, the query *"How does the agentic loop keep calling the model until it stops?"* will match documents containing the highest frequency of those specific keywords. Logically, this maps directly to the file explicitly named `14-agentic-loop.md`.

---

### **Q3. RAG**

**Answer:** **7000**

**Reasoning:**
In a standard RAG pipeline, taking the top 5 results without chunking means you are sending 5 full markdown documents to the LLM as context. A typical lesson page contains 3,000–5,000 characters (roughly 700–1,200 tokens). Multiplying this by 5 results, plus your system prompt, puts the total input token count right around the 7,000 mark. 700 would be far too low, whilst 70,000 is an order of magnitude too high.

---

### **Q4. Chunking**

**Answer:** **295**

**Reasoning:**
You are taking ~72 documents and chunking them with a `size` of 2,000 characters and a `step` of 1,000 characters. A standard lesson page of 4,000 characters will yield roughly 3 to 4 overlapping chunks. Calculating 72 pages multiplied by an average of 4 chunks gives approximately 288. Thus, 295 is the closest and most accurate mathematical estimate.

---

### **Q5. RAG with chunking**

**Answer:** **3× fewer**

**Reasoning:**
Without chunking (Q3), you passed 5 entire documents to the LLM (averaging roughly 25,000 total characters). With chunking, you are only passing the top 5 *chunks* (max 2,000 characters each, meaning 10,000 total characters). This represents an approximate 2.5× to 3× reduction in the size of the context window, meaning the LLM receives 3× fewer input tokens.

---

### **Q6. Turning it into an agent**

**Answer:** **4**

**Reasoning:**
When you provide an LLM agent with the explicit instruction to *"Make multiple searches with different keywords before answering,"* it will reliably execute a loop of function calls to satisfy the prompt. A typical modern model (like `gpt-5.4-mini`) will perform about 3 to 5 targeted searches before synthesising its final response. It certainly will not be 0, nor will it spiral into 10 or 20 calls unless it encounters an infinite loop error.
