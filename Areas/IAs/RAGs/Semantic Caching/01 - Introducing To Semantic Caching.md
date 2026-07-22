---
tipo: aula
area: IAs
tags:
- ai
- llm
- caching
- redis
- performance
- course/deeplearningai
- ia/rag
criada: '2025-11-26'
status: 📝 In Progress
source: Semantic Caching for AI Agents (Redis)
---

# Introduction to Semantic Caching

This note covers the fundamentals of the "Semantic Caching for AI Agents" course, focusing on solving latency and cost issues in Generative AI applications using Redis.

## 🎯 The Problem: Scale and Cost
In many AI projects, two factors limit application scalability:
1.  **Inference Costs:** Repeatedly calling LLMs is expensive.
2.  **Latency:** Model response times can be high, affecting user experience.

## 💡 Traditional vs. Semantic Caching

### Traditional Cache (Exact Match)
Works only when the input text is **exactly the same**.
* *Example:*
    * User A: "How can I get a refund?"
    * User B: "I want my money back."
    * **Result:** Traditional cache sees them as different inputs and calls the model twice.

### Semantic Cache
Analyzes the **meaning** (semantics) of the question.
* Uses **Embeddings** to measure similarity between two queries in a vector space.
* If semantic similarity reaches a defined **threshold**, the system reuses an old response.



> [!INFO] Key Benefit
> Semantic Caching allows reusing model responses for questions with **different phrasing** but the **same intent**.

---

## 📚 Learning Roadmap (Course Structure)

The course is divided into progressive implementation and optimization stages:

### 1. Building from Scratch (Under the hood)
* Creating **Embeddings**.
* Calculating **distance** (similarity).
* Setting a **Threshold** to decide when two queries are "similar enough".

### 2. Implementation with Redis (Production)
Using Redis open-source SDK to move closer to a production scenario.
* **TTL (Time to Live):** To keep the cache fresh and small.
* **Multi-tenancy:** Separate caches for different users, teams, or tenants.
* Using open-weight embedding models fine-tuned for cache accuracy.

### 3. Performance Metrics
How to measure if the cache is helping or hindering.
* **Hit Rate:** How often the cache is used.
* **Precision & Recall:** How often the cache is correct vs. comprehensive.
* **Latency:** Measuring accumulated time savings.

> [!NOTE] Analysis Tool
> Using a **Confusion Matrix** to visualize how changing the *similarity threshold* shifts the balance between precision and recall.



[Image of confusion matrix precision recall]


### 4. Enhancements (Optimization)
Four methods to refine the cache:
1.  **Threshold Optimization:** Fine-tuning the similarity limit.
2.  **Cross-Encoder:** Used for *re-ranking* and better comparison accuracy.
3.  **LLM Check:** A small LLM check to confirm if two questions mean the same thing.
4.  **Fuzzy Matching:** Handling simple typos before semantic search.

### 5. Integration with AI Agents
Connecting the cache inside an Agent workflow.
* The agent breaks big questions into smaller parts.
* Checks the cache for each part.
* Calls the LLM only when necessary (cache miss).
* **Effect:** As the cache "warms up", model calls drop, and speed increases.

---

## 🔗 References
* **Real Use Case:** The course covers techniques published by **Walmart** to improve their production caching system.
* **Instructors:** Tyler Hutcherson and Iliya Zhechev (Redis).