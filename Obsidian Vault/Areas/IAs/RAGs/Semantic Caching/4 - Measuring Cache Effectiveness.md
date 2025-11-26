---
tags:
  - AI
  - Metrics
  - Performance
  - Latency
  - Evaluation
  - Lab
status: ✅ Completed
source: Semantic Caching for AI Agents (Lesson 3/4)
---

# Measuring Cache Effectiveness

In this lesson, we learn how to evaluate a semantic cache using standard Machine Learning metrics. A cache can fail in two ways: **Low Quality** (wrong answers) or **Poor Performance** (too slow).

## 📊 Part 1: Quality Metrics (Accuracy)

To measure quality, we treat the cache like a classification model. We look at **Precision** and **Recall**, derived from a Confusion Matrix.

### Precision vs Recall

#### 1. Precision (The Quality) 

**"When the cache says 'I found a match', is it actually correct?"** 

**Definition:** The percentage of retrieved instances (Cache Hits) that were actually relevant (Correct). 

**The Risk:** Low precision means your system is generating **False Positives**. * *Example:* User asks "How do I return a shirt?", and the cache returns an answer for "How do I buy a shirt?". The user gets the wrong info. 

**Formula:** $$Precision = \frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}$$
> [!TIP] Memory Aid
> High Precision = **"I trust you."** . The system rarely makes mistakes when it speaks

![[Pasted image 20251126122200.png]]

![[Pasted image 20251126124027.png]]
## 2. Recall (The Quantity) 

**"Of all the correct answers that exist in the cache, how many did we find?"** 

**Definition:** The percentage of relevant instances that were successfully retrieved. 

 **The Risk:** Low recall means your system is generating **False Negatives**. * *Example:* The answer for "Refunds" was in the cache, but the system didn't think it was similar enough to the user's question, so it treated it as a miss and called the expensive LLM. 

**Formula:** $$Recall = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}$$


> [!TIP] Memory Aid
> High Recall = **"I hear you."** (The system catches most opportunities to save money).


#### The Confusion Matrix in Caching
* **True Positive (TP):** The query matched a cached entry, and it was a *correct* match.
* **True Negative (TN):** The query did *not* match anything, and there was indeed nothing relevant in the cache.
* **False Positive (FP):** The query matched a cached entry, but it was **wrong** (bad answer).
    * *Risk:* User gets incorrect info.
* **False Negative (FN):** The query did *not* match, but it **should have**.
    * *Risk:* Unnecessary cost (cache miss) when we had the answer.

### The Trade-off: Precision vs. Recall (The Threshold)

You cannot usually maximize both simultaneously; there is a "tug-of-war" controlled by your **Distance Threshold**. 

**Stricter Threshold** (e.g., Distance < 0.1) | "Only accept if it's almost identical." > **Result:** High Precision (very accurate), but Low Recall (you miss slightly phrased variations).

**Loose Threshold** (e.g., Distance < 0.5) | "Accept if it seems vaguely similar" >  **Low Precision** (Risk of wrong answers). **High Recall** (Catches everything) 

The F1 Score To find the "sweet spot" between Precision and Recall, we use the F1 Score (the harmonic mean of the two). $$F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}$$

The **Distance Threshold** controls this balance:

| Action | Effect on Precision | Effect on Recall |
| :--- | :--- | :--- |
| **Lower Threshold** (Stricter) | ⬆️ Increases | ⬇️ Decreases (More Misses) |
| **Raise Threshold** (Looser) | ⬇️ Decreases (Risk of FP) | ⬆️ Increases |

![[Pasted image 20251126124158.png]]


> [!TIP] F1 Score
> To find the "sweet spot" (best threshold), we often use the **F1 Score**, which is the harmonic mean of Precision and Recall.

---

## ⚡ Part 2: Performance Metrics (Latency)

We need to prove that the cache actually speeds up the system. We calculate the **Expected System Latency**.

### The Formula
$$L_{sys} = (L_{cache} \times R) + (L_{llm} + L_{cache}) \times (1 - R)$$

Where:
* $L_{sys}$: Average Latency of the whole system.
* $L_{cache}$: Average cache latency.
* $L_{llm}$: Average Latency of an LLM Call.
* $R$: Cache Hit Ratio (percentage).

**Example:**
* Cache Latency: 11ms
* LLM Latency: 350ms
* Hit Rate: 30%
* **Result:** The system average drops to ~256ms (a 26% improvement).

---

## 🤖 Part 3: LLM-as-a-Judge

How do we know if a cache hit is "True" or "False" without checking every row manually? We use an **LLM-as-a-Judge**.

1.  **Full Retrieval:** Run queries against the cache with a very high threshold (e.g., 1.0) to find the *closest* neighbor, no matter how far.
2.  **Evaluation:** Send the pair (User Query + Cached Question) to a strong LLM (like GPT-4).
3.  **Prompt:** *"Do these two questions mean the same thing? Yes/No."*
4.  **Labeling:** Use the LLM's "Yes/No" response as the Ground Truth label to calculate Precision/Recall.

---

## 💻 Part 4: Lab Implementation

Below is the complete code for setting up the environment, evaluating quality/latency, and implementing the LLM-as-a-Judge workflow.

### 1. Setup & Data Loading
```python
# Warning control
import warnings
warnings.filterwarnings('ignore')

import pandas as pd
import numpy as np
import time
from tqdm.auto import tqdm

# Import Course Helpers
from cache.evals import CacheEvaluator
from cache.faq_data_container import FAQDataContainer
from cache.wrapper import SemanticCacheWrapper
from cache.config import config, load_openai_key

print("📦 Libraries imported successfully")

# Load Data
data_container = FAQDataContainer()
faq_df, test_df = data_container.faq_df, data_container.test_df
test_queries = test_df["question"].tolist()

# Initialize Cache Wrapper
cache_wrapper = SemanticCacheWrapper.from_config(config)
```

### 2. Evaluatin cache quality (recall/precision)

```python
# Hydrate Cache
cache_wrapper.hydrate_from_df(faq_df)

# Check a sample
print(f"Sample Check: {cache_wrapper.check(faq_df['question'].iloc[0])}")

# Run all test queries
cache_results = cache_wrapper.check_many(test_queries)

# Evaluate using pre-defined ground truth labels (from dataset)
evaluator = CacheEvaluator(
    true_labels=data_container.label_cache_hits(cache_results),
    cache_results=cache_results,
)
evaluator.report_metrics()

# Inspecting Confusion Matrix Groups
metrics = evaluator.get_metrics()
[[tn, fp], [fn, tp]] = metrics["confusion_mask"]

# View False Positives (Where the cache matched, but was wrong)
print("False Positives Examples:")
print(evaluator.matches_df()[fp])
```

### 3. Evaluating Latency

```python
# Mock function to simulate LLM slowness
def simulate_llm_call(prompt):
    time.sleep(np.random.uniform(0.2, 0.5)) # Sleeps 200-500ms
    return f"LLM response to {prompt}"

from cache.evals import PerfEval
perf_eval = PerfEval()

# Run Loop: Check Cache -> If Hit (Track) -> Else Call Mock LLM (Track)
with perf_eval:
    for query in tqdm(test_queries):
        cache_wrapper.check(query)
        perf_eval.tick("cache_hit")
        
        # Simulate LLM call for comparison
        perf_eval.start()
        simulate_llm_call(query)
        perf_eval.tick("llm_call")

metrics = perf_eval.get_metrics(labels=["cache_hit", "llm_call"])

# Visualize
perf_eval.plot(title="Performance Comparison", show_cost_analysis=False)

# Calculate Theoretical Speedup
llm_latency = metrics["by_label"]["llm_call"]["average_latency"]
cache_latency = metrics["by_label"]["cache_hit"]["average_latency"]
cache_hit_rate = 0.3 # Assumption

cached_llm_latency = llm_latency * (1 - cache_hit_rate) + cache_latency * cache_hit_rate
cached_llm_drop_in_latency = (llm_latency - cached_llm_latency) / llm_latency
cached_llm_speedup = llm_latency / cached_llm_latency

print(f"Overall latency drop: {int(cached_llm_drop_in_latency * 100)}%")
print(f"Overall speedup: {cached_llm_speedup:.2f}x")
```

### 4. LLM-as-a-judge (Automated Labeling)

```python
# 1. Reset and perform Full Retrieval (Threshold=1.0) to get pairs
cache_wrapper.hydrate_from_df(faq_df)
full_retrieval_nearest_neighbors = cache_wrapper.check_many(
    test_queries, distance_threshold=1
)
full_retrieval_matches = [h.matches[0].prompt for h in full_retrieval_nearest_neighbors]

# 2. Load OpenAI Key
load_openai_key()

# 3. Use LLM to Judge Similarity
from cache.llm_evaluator import LLMEvaluator

evaluator_llm = LLMEvaluator.construct_with_gpt()

# Predict: "Are these pairs similar?"
llm_similarity_results = evaluator_llm.predict(
    dataset=zip(test_queries, full_retrieval_matches),
    batch_size=5,
)

print(llm_similarity_results.df.head())

# 4. Re-Evaluate Metrics based on LLM Labels
evaluator = CacheEvaluator.from_full_retrieval(
    true_labels=llm_similarity_results.df["is_similar"].values,
    cache_results=cache_wrapper.check_many(test_queries),
)
evaluator.report_metrics()

# Cleanup
cache_wrapper.cache.clear()
```

