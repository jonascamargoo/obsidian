---
tags:
  - AI
  - Python
  - Redis
  - VectorSearch
  - Implementation
  - Performance
status: 📝 In Progress
source: Semantic Caching for AI Agents (Lesson 3)
---
---
tags:
  - AI
  - Python
  - Redis
  - CodeSnippet
  - Implementation
  - Lab
status: ✅ Completed
source: Semantic Caching for AI Agents (Lab 2)
---

# Lab: Building Semantic Cache (From Scratch vs. Redis)

In this lab, we bridge the gap between theory and practice. We first implement the semantic cache logic manually using **NumPy** to understand the vector mathematics, and then we migrate to a production-ready solution using **Redis** and `redisvl`.

## 🧠 Part 1: The "From Scratch" Approach (Mental Model)

Before using a database, we simulate the cache using local memory (Pandas/NumPy).

### 1. The Data
We use a Customer Support FAQ dataset.
* **Input:** User questions (Queries).
* **Output:** Standardized answers.

### 2. The Logic: Cosine Similarity
To find if a new question matches an old one, we calculate the **Cosine Distance**.
* **Embeddings:** We convert text into vectors using `all-mpnet-base-v2`.
* **Threshold:** We set a strict limit (e.g., `0.3`).
    * If `distance < 0.3` → **HIT** (Reuse answer).
    * If `distance > 0.3` → **MISS** (New question).

> [!TIP] Math Refresher
> Cosine distance is calculated as:
> $$1 - \frac{A \cdot B}{||A|| \times ||B||}$$
> The closer the result is to 0, the more similar the vectors are.

---

## 🚀 Part 2: Production Implementation (Redis)

Local arrays don't scale. We move the logic to **Redis** using the `redisvl` library.

### Key Components
1.  **Redis Connection:** Standard connection string (`redis://localhost:6379`).
2.  **Specialized Model:** We switch to `langcache-embed-v1`.
    * *Why?* This model is fine-tuned specifically for caching tasks, offering better accuracy than generic models.
3.  **TTL (Time To Live):** We set an eviction policy (e.g., 24 hours) so the cache doesn't grow infinitely with old data.

---

## 📊 Part 3: Performance Benchmark

We run an end-to-end test comparing the Cache against a direct LLM call (`gpt-4o-mini`).

| Metric | Cache HIT | Cache MISS (LLM Call) |
| :--- | :--- | :--- |
| **Speed** | ~65 ms | > 1,000 ms |
| **Cost** | $0.00 | $ per token |

> [!SUCCESS] Conclusion
> The semantic cache provided a **15x speed improvement** for repeated queries.

---

## 📂 Appendix: Full Lab Code

Below is the complete code workflow from the lab notebook, formatted for copying.

### 1. Setup & Data Loading
```python
# Warning control
import warnings
warnings.filterwarnings('ignore')

# Load the FAQ Dataset
import pandas as pd
import numpy as np
import time
from cache.faq_data_container import FAQDataContainer

faq_data = FAQDataContainer()
faq_df = faq_data.faq_df
test_df = faq_data.test_df

# Display first rows (Notebook style)
# faq_df.head().style 
print(faq_df.head())
```

## 2 - Manual Implementation (numpy)

``` python
# Create Embeddings for Semantic Search
from sentence_transformers import SentenceTransformer

encoder = SentenceTransformer("all-mpnet-base-v2")
faq_embeddings = encoder.encode(faq_df["question"].tolist())

print(f"Sample (first 10 dimensions): {faq_embeddings[0][:10]}")

# Implement Semantic Search Math
def cosine_dist(a: np.array, b: np.array):
    """Compute cosine distance between two sets of vectors."""
    a_norm = np.linalg.norm(a, axis=1)
    b_norm = np.linalg.norm(b) if b.ndim == 1 else np.linalg.norm(b, axis=1)
    sim = np.dot(a, b) / (a_norm * b_norm)
    return 1 - sim

def semantic_search(query: str) -> tuple:
    """Find the most similar FAQ question to the query."""
    query_embedding = encoder.encode([query])[0]
    distances = cosine_dist(faq_embeddings, query_embedding)

    # Find the most similar question (lowest distance)
    best_idx = int(np.argmin(distances))
    best_distance = distances[best_idx]

    return best_idx, best_distance

# Test the search
idx, distance = semantic_search("How long will it take to get a refund for my order?")
print(f"Most similar FAQ: {faq_df.iloc[idx]['question']}")
print(f"Answer: {faq_df.iloc[idx]['answer']}")
print(f"Cosine distance: {distance:.3f}")
```

## 3 - Building the simple cache function

```python
def check_cache(query: str, distance_threshold: float = 0.3):
    """
    Semantic cache lookup for previously asked questions.
    Returns a dictionary with answer if hit, None if miss.
    """
    idx, distance = semantic_search(query)

    if distance <= distance_threshold:
        return {
            "prompt": faq_df.iloc[idx]["question"],
            "response": faq_df.iloc[idx]["answer"],
            "vector_distance": float(distance),
        }
    return None  # Cache miss

# Test Queries
test_queries = [
    "Is it possible to get a refund?",
    "I want my money back",
    "What are your business hours?",  # Should miss
]

for query in test_queries:
    result = check_cache(query, distance_threshold=0.3)
    if result:
        print(f"✅ HIT: '{query}' -> {result['response'][:50]}...")
        print(f"   Distance: {result['vector_distance']:.3f}\n")
    else:
        print(f"❌ MISS: '{query}'\n")
```

## 4 - Updating the cache (dynamic)

```python
def add_to_cache(question: str, answer: str):
    """
    Add a new Q&A pair to our simple in-memory cache.
    Extends both the DataFrame and embeddings matrix.
    """
    global faq_df, faq_embeddings

    new_row = pd.DataFrame({"question": [question], "answer": [answer]})
    faq_df = pd.concat([faq_df, new_row], ignore_index=True)

    # Generate embedding for the new question
    new_embedding = encoder.encode([question])

    # Add to embeddings matrix
    faq_embeddings = np.vstack([faq_embeddings, new_embedding])

    print(f"✅ Added to cache: '{question}'")

# Adding new entries
new_entries = [
    ("What are your business hours?", "We're open Monday-Friday 9 AM to 6 PM EST..."),
    ("Do you have a mobile app?", "Yes! Our mobile app is available on both iOS and Android..."),
    ("How do I update my payment method?", "Go to Account Settings > Payment Methods..."),
]

for question, answer in new_entries:
    add_to_cache(question, answer)

print(f"\nCache now has {len(faq_df)} total entries")
```

## 5 - Moving to Redis

```python
import os
import redis

# Redis Connection
REDIS_URL = os.getenv("REDIS_URL", "redis://localhost:6379")

try:
    r = redis.Redis.from_url(REDIS_URL)
    r.ping()
    print("✅ Redis is running and accessible")
except redis.ConnectionError:
    print("❌ Cannot connect to Redis")
    raise

# Using Cache-Optimized Model
from redisvl.utils.vectorize import HFTextVectorizer
from redisvl.extensions.cache.embeddings import EmbeddingsCache

langcache_embed = HFTextVectorizer(
    model="redis/langcache-embed-v1",
    cache=EmbeddingsCache(redis_client=r, ttl=3600)
)

# Create the Redis Semantic Cache
from redisvl.extensions.cache.llm import SemanticCache

cache = SemanticCache(
    name="faq-cache",
    vectorizer=langcache_embed,
    redis_client=r,
    distance_threshold=0.3
)

# Load the Cache with FAQ Data
for i in range(len(faq_df)):
    cache.store(
        prompt=faq_df.iloc[i]["question"],
        response=faq_df.iloc[i]["answer"]
    )

# Quick Check
result = cache.check("I need a refund for my purchase")
print(result)

# Implement TTL (Time-To-Live)
cache.set_ttl(86400) # 1 Day
```

## 6 - End-to-End LLM

```python
from cache.config import load_openai_key
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage
from cache.evals import PerfEval

load_openai_key()
MODEL_NAME = "gpt-4o-mini"

llm = ChatOpenAI(
    model=MODEL_NAME,
    temperature=0.1,
    max_tokens=150,
)

def get_llm_response(question: str) -> str:
    prompt = f"""
    You are a helpful customer support assistant. Answer this customer question concisely:
    Question: {question}
    """
    response = llm.invoke([HumanMessage(content=prompt)])
    return response.content.strip()

# Performance Evaluation
perf_eval = PerfEval()
test_questions = [
    "How can I get my money back?",
    "I want a refund please",
    "What's your return policy?",
    "I forgot my password",
    "Can you help me reset my password?",
    # ... (more questions)
]

perf_eval.set_total_queries(len(test_questions))

with perf_eval:
    for i, question in enumerate(test_questions, 1):
        print(f"\n[{i}] Question: '{question}'")
        perf_eval.start()

        if cached_result := cache.check(question):
            # Cache HIT
            perf_eval.tick("cache_hit")
            print(f"    ✅ CACHE HIT (distance: {cached_result[0]['vector_distance']:.3f})")
        else:
            # Cache MISS
            perf_eval.tick("cache_miss")
            print(f"    ❌ CACHE MISS -> Calling LLM...")
            
            perf_eval.start()
            llm_response = get_llm_response(question)
            perf_eval.tick("llm_call")
            perf_eval.record_llm_call(MODEL_NAME, question, llm_response)
            
            # Store in cache
            cache.store(prompt=question, response=llm_response)

# Final Stats
print(f"Mean Cache Hit Time: {np.mean(perf_eval.durations_by_label['cache_hit'])}")
print(f"Mean LLM Call Time: {np.mean(perf_eval.durations_by_label['llm_call'])}")
```

