---
description: TARTReranker Class Documentation
---

# TART Reranker

## Overview

The `TARTReranker` class is a reranker based on [TART](https://arxiv.org/pdf/2211.09260.pdf). It is designed to rerank passages using specific instructions. The primary functionality of this class lies in its ability to rerank a list of passages based on a given query and instruction.&#x20;

## Usage

### Initialize

To use the `TARTReranker` class, start by creating an instance of the class with an instruction that will be used to guide the reranking process. This is done by passing the instruction as a string to the `TARTReranker` constructor during initialization.

```python
from RAGchain.reranker import TARTReranker

reranker = TARTReranker(instruction="Find passage to answer given question")
```

In this example, "Find passage to answer given question" is the instruction that will be used for reranking. You can put any instructions like "Find python code implementation of user's question." or "Find specific name of Python class."

### rerank

After the `TARTReranker` instance has been initialized, you can use the `rerank` method to rerank a list of passages based on a given query. The `rerank` method takes two parameters: a query (a string), and a list of passages.

```python
query = "What is query decomposition?"
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier

reranked_passages = reranker.rerank(query, passages)
print(reranked_passages)
```

The `rerank` method returns a new list of the passages, reordered based on the given instruction and query.
