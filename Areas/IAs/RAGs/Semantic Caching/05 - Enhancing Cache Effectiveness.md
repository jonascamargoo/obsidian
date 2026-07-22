---
tipo: aula
area: IAs
tags:
- ia/rag
criada: '2025-11-26'
---

---
tags:
  - AI
  - Optimization
  - Reranking
  - CrossEncoder
  - FuzzyMatching
  - Lab
status: ✅ Completed
source: Semantic Caching for AI Agents (Lesson 4)
---

# Enhancing Cache Quality

In this lesson, we explore four advanced strategies to improve the accuracy (Precision & Recall) of our Semantic Cache. We move beyond simple vector distance to more sophisticated verification methods.

## 📈 Strategy 1: Threshold Sweep (Optimization)
Finding the perfect "Distance Threshold" is an optimization problem.
* **Goal:** Maximize the **F1 Score** (Balance between Precision and Recall).
* **Method:** We test the cache against a validation set using a range of thresholds (e.g., 0.1 to 0.9).
* **Visual:**
    * As Threshold increases ➡ Recall ⬆️, Precision ⬇️.
    * The F1 Score peaks at the intersection (intermediate value).


![[Pasted image 20251126152609.png]]


---

## 🔁 Strategy 2: Cross-Encoder (Reranking)
Embeddings are fast but lose nuance because they compress sentences into single vectors independently.
* **What is it?** A model that processes two sentences *simultaneously* to output a similarity score.
	![[Pasted image 20251126152640.png]]
* **Pros:** Highly accurate; understands context better than embeddings.
* **Cons:** Slower (computationally expensive).
* **Workflow:**
    1.  Query the 10 closest cache hits
    2.  Run the query and the cache hits through the cross encoder
	    1. You obtain a new scores, hence reranking
    3.  Return the entry with the highest cross-encoder score

![[Pasted image 20251126152952.png]]

> [!EXAMPLE] Nuance Check
> *Sentence A:* "The bank raised interest rates."
> *Sentence B:* "The river overflowed near the bank."
> *Embedding Model:* Might think they are similar (keyword "bank").
> *Cross-Encoder:* Knows they are different contexts (Financial vs. River).

---

## 🤖 Strategy 3: LLM Check (Validator)
Using a lightweight LLM to verify the match before returning it to the user.
![[Pasted image 20251126153123.png]]
* **Method:** Ask an LLM: *"Are these two sentences semantically equivalent? Yes/No."*
* **Use Case:** Can be used as a final "Gatekeeper" to eliminate False Positives (Incorrect Hits).
* **Trade-off:** Increases latency significantly compared to pure vector search, but guarantees near 100% precision.

---

## ⌨️ Strategy 4: Fuzzy Matching (Typos)
Handling simple errors before they even reach the embedding model.
![[Pasted image 20251126153849.png]]
* **Technique:** Measures **Edit Distance** (Deletions, Substitutions, Insertions).
* **Why?** Embeddings can sometimes be confused by severe typos. Fuzzy matching catches "refudn" -> "refund".
* **Placement:** Placed **in front** of the semantic cache. If a fuzzy match is found (high confidence), we short-circuit the vector search.

---

## 💻 Lab Implementation

Below is the code to implement these four strategies.

### 1. Setup & Baseline
```python
import warnings
warnings.filterwarnings('ignore')
import matplotlib.pyplot as plt
import seaborn as sns
from cache.config import config
from cache.wrapper import SemanticCacheWrapper
from cache.faq_data_container import FAQDataContainer
from cache.evals import CacheEvaluator

# Initialize Wrapper & Data
cache_wrapper = SemanticCacheWrapper.from_config(config)
data_container = FAQDataContainer()
test_queries = data_container.test_df["question"].tolist()

# Baseline Hydration (Standard 0.3 threshold)
cache_wrapper.hydrate_from_df(data_container.faq_df)
cache_results = cache_wrapper.check_many(test_queries, distance_threshold=0.3)

# Initial Baseline Report
evaluator = CacheEvaluator(
    true_labels=data_container.label_cache_hits(cache_results),
    cache_results=cache_results,
)
evaluator.report_metrics()
```

### 2. Threshold Sweep (Finding the sweet spot)

```python
# 1. Perform Full Retrieval (Threshold=1.0)
cache_results = cache_wrapper.check_many(test_queries, distance_threshold=1)

# 2. Initialize Evaluator
evaluator = CacheEvaluator.from_full_retrieval(
    true_labels=data_container.label_cache_hits(cache_results),
    cache_results=cache_results,
)

# 3. Automatic Sweep (Maximize F1)
evaluator.report_threshold_sweep(
    metric_to_maximize="f1_score",
    metrics_to_plot=["f1_score", "precision", "recall"],
)
```

### 3. Cross-Encoder Reranking

```python
from cache.cross_encoder import CrossEncoder

# Initialize Model (Alibaba-NLP modernbert-base)
cross_encoder = CrossEncoder("Alibaba-NLP/gte-reranker-modernbert-base")

# Register Reranker to Cache Wrapper
cache_wrapper.register_reranker(cross_encoder.create_reranker())

# Check Improvement
cache_results = cache_wrapper.check_many(
    test_queries,
    distance_threshold=1,
    num_results=10, # Retrieve Top 10 for Reranking
    use_reranker_distance=True,
)

evaluator = CacheEvaluator.from_full_retrieval(
    true_labels=data_container.label_cache_hits(cache_results),
    cache_results=cache_results,
)
evaluator.report_threshold_sweep()
```

### 4. LLM Validator (high precision)

```python
from cache.llm_evaluator import LLMEvaluator
from cache.config import load_openai_key

load_openai_key()

# Construct LLM Validator
llm = LLMEvaluator.construct_with_gpt()

# Switch Reranker to LLM
cache_wrapper.clear_reranker()
cache_wrapper.register_reranker(llm.create_reranker(batch_size=4))

# Check with optimal threshold found earlier (e.g., 0.28)
cache_results = cache_wrapper.check_many(
    test_queries,
    distance_threshold=0.2828,
    num_results=1,
    show_progress=True,
)

evaluator = CacheEvaluator.from_full_retrieval(
    true_labels=data_container.label_cache_hits(cache_results),
    cache_results=cache_results,
)
evaluator.report_metrics()
# Expectation: 100% Precision (No False Positives)
```

### 5. Fuzzy Matching

```python
import numpy as np

# Helper to generate typos (noise)
def fuzzify_string(str, its=3):
    for i in range(its):
        str_list = list(str)
        i = np.random.randint(0, len(str) - 1)
        try:
            str_list[i], str_list[i + 1] = str_list[i + 1], str_list[i]
        except IndexError: pass
        str = "".join(str_list)
    return str

# Generate noisy queries
fuzzy_queries = []
for q in data_container.faq_df["question"].tolist():
    for difficulty in [2, 3, 4, 10]:
        fuzzy_queries.append(fuzzify_string(q, difficulty))

# Use FuzzyCache Implementation
from cache.fuzzy_cache import FuzzyCache

fuzzy_cache = FuzzyCache()
fuzzy_cache.hydrate_from_df(data_container.faq_df)
fuzzy_retrievals = fuzzy_cache.check_many(fuzzy_queries)

# Check Results
print(fuzzy_retrievals[:5])

# Cleanup
cache_wrapper.cache.clear()
```

