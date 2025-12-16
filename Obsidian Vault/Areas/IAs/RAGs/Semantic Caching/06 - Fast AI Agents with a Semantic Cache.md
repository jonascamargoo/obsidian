---
tags:
  - AI
  - Agents
  - LangGraph
  - Architecture
  - RAG
  - Implementation
status: ✅ Completed
source: Semantic Caching for AI Agents (Lesson 5/6)
---
https://learn.deeplearning.ai/courses/semantic-caching-for-ai-agents/lesson/rmm0g6/fast-ai-agent-with-semantic-cache
# Integrating Semantic Cache into AI Agents

In this final lesson, we combine everything to build a **Deep Research Agent**. 

## 🤖 The Problem: Token-Hungry Agents
Agents are expensive to scale because they are iterative. A single user request might trigger:
1.  Query Decomposition (Planning)
2.  Tool Calling (Research)
3.  Reflection (Self-Correction)
4.  Synthesis

If a user asks a slightly different version of a question the agent solved yesterday, re-running all these steps is a waste of money and time.

## 🏗️ The Solution: Granular Caching in LangGraph

Instead of just caching the final answer, we cache **intermediate states** and **sub-questions**.

### The Workflow Architecture
We use **LangGraph** to define a cognitive architecture with the following nodes:

1.  **Decompose:** Break the user's complex query into 3-5 sub-questions.
2.  **Check Cache:** Check the Semantic Cache for *each* sub-question individually.
    * *Hit:* Retrieve answer instantly.
    * *Miss:* Send to Research queue.
3.  **Research (RAG):** Query the Knowledge Base (Vector DB) for missing info.
4.  **Evaluate (Quality Loop):** An "LLM Judge" scores the research quality (0-1). If poor, iterate and research again.
5.  **Synthesize:** Combine cached answers + new research into a final response.

### Visualizing the Flow

![[Pasted image 20251126155011.png]]

## 🚀 Performance: The "Learning" Effect

The lesson demonstrates how the agent becomes faster and cheaper over time as it processes similar scenarios.

|**Scenario**|**State**|**Cache Hit Rate**|**Latency**|**LLM Calls**|
|---|---|---|---|---|
|**1. Cold Start**|New Query|**25%**|~20s|8 Calls|
|**2. Partial Match**|Similar Context|**75%**|~13s|4 Calls|
|**3. Warm Cache**|Heavy Overlap|**75%**|~18s|6 Calls|
## 💻 Lab Implementation: The Deep Research Agent

### 1. Setup & Dependencies

```python
import warnings
warnings.filterwarnings('ignore')
import logging
from agent import set_openai_key

set_openai_key()

# Logging Setup
logging.basicConfig(level=logging.INFO, format="%(asctime)s | %(levelname)s | %(message)s")
logger = logging.getLogger("agentic-workflow")

# Redis Connection
import redis
redis_client = redis.Redis.from_url("redis://localhost:6379", decode_responses=False)
redis_client.ping()
```

### 2. Building the knowledge base (cache miss)

```python
from redisvl.utils.vectorize import OpenAITextVectorizer
from agent import create_knowledge_base_from_texts

embeddings = OpenAITextVectorizer()

raw_docs = [
    "Our premium support plan includes 24/7 phone support...",
    "API rate limits by plan: Free 100/hr, Pro 10,000/hr...",
    "Security features: SOC2 compliance, GDPR...",
    # ... (Add more documents here)
]

# Create Index in Redis
success, message, kb_index = create_knowledge_base_from_texts(
    texts=raw_docs,
    source_id="customer_support_docs",
    redis_url="redis://localhost:6379",
    skip_chunking=True
)
```

### 3. Initialize the semantic cache

```python
from cache.wrapper import SemanticCacheWrapper
from cache.config import config
from cache.faq_data_container import FAQDataContainer

cache = SemanticCacheWrapper.from_config(config)
data = FAQDataContainer()

# Optional: Pre-load (Hydrate) with some FAQ data
cache.hydrate_from_df(data.faq_df, clear=True)
```

### 4. Defining the LangGraph Workflow

```python
from langgraph.graph import StateGraph, END
from agent import (
    WorkflowState, initialize_agent, decompose_query_node, 
    check_cache_node, research_node, evaluate_quality_node, 
    synthesize_response_node, route_after_cache_check, 
    route_after_quality_evaluation
)

# Initialize global agent tools
initialize_agent(cache, kb_index, embeddings)

# Define Graph
workflow = StateGraph(WorkflowState)

# Add Nodes
workflow.add_node("decompose_query", decompose_query_node)
workflow.add_node("check_cache", check_cache_node)
workflow.add_node("research", research_node)
workflow.add_node("evaluate_quality", evaluate_quality_node)
workflow.add_node("synthesize", synthesize_response_node)

# Entry Point
workflow.set_entry_point("decompose_query")

# Add Edges (Logic Flow)
workflow.add_edge("decompose_query", "check_cache")

# Conditional Edge: If Cache Hit -> Skip Research
workflow.add_conditional_edges(
    "check_cache",
    route_after_cache_check,
    {
        "research": "research", 
        "synthesize": "synthesize",
    },
)

workflow.add_edge("research", "evaluate_quality")

# Conditional Edge: If Quality Bad -> Retry Research
workflow.add_conditional_edges(
    "evaluate_quality",
    route_after_quality_evaluation,
    {
        "research": "research",
        "synthesize": "synthesize",
    },
)

workflow.add_edge("synthesize", END)

# Compile
workflow_app = workflow.compile()
```

### 5. Running the agent (Scenarios)

```python
from agent import run_agent, display_results, analyze_agent_results

# Scenario 1: Evaluation (Cold Start)
query_1 = "I need to understand your security standards (SOC2) and API rate limits for the Pro plan."
result1 = run_agent(workflow_app, query_1)
display_results(result1)

# Scenario 2: Planning (Similar topics, should hit cache)
query_2 = "Moving forward with planning. Compare API limits for Pro vs Enterprise and confirm security again."
result2 = run_agent(workflow_app, query_2)
display_results(result2)

# Analyze Performance Improvements
total_questions, total_cache_hits = analyze_agent_results([result1, result2])
```

### 6. Interactive Demo (Optional)

```python
from agent import launch_demo

launch_demo(
    workflow_app,
    cache,
    share=True,
    inline=True
)
```

