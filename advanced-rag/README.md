---
description: For making advanced RAG workflow. Several tips and useful utils will be introduced.
---

# For Advanced RAG

This section introduces techniques and utilities for creating advanced Retrieval-Augmented Generation (RAG) workflows
using RAGchain.
In RAGchain, we delve into the complexities of constructing production-level RAG workflows.
It's challenging to create a flawless RAG workflow tailored to your specific needs.
However, certain patterns can enhance the effectiveness of these workflows, so we prepare patterns that you might need.

We are continually developing and improving this framework, so expect further updates.

## Time-Aware RAG

In real-world applications, you'll often find that the latest information is more valuable than outdated data.
However, manually discarding old information can be challenging and potentially harmful, as this information might be
useful for other queries.
Therefore, time-aware RAG is crucial for certain applications.

Time-aware RAG prioritizes recent information without discarding older data that might still be relevant.
To learn how to implement time-aware RAG in RAGchain, please refer to [Time-Aware RAG](./time_aware_rag.md).

## Importance-Aware RAG

In some cases, you may want to prioritize certain passages over others.
For example, when you try to find specific information at Google search, there are some websites that you trust more
than others.
Or, some websites that you don't want to see.
In this case, you can use importance-aware RAG.

Importance-aware RAG prioritizes certain passages over others. 
To learn how to implement importance-aware RAG in RAGchain,
please refer to [Importance-Aware RAG](./importance_aware_rag.md).
