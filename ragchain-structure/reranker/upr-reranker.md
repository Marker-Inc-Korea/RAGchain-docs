# UPR Reranker

## Overview

The `UPRReranker` class is a reranker based on paper called "[Improving Passage Retrieval with Zero-shot Question Generation](https://arxiv.org/abs/2204.07496)". It uses a language model to generate a question based on the passage and reranks the passages by the likelihood of the question.&#x20;

It can enhance accuracy because it calculates likelihood original passages and related passages (generated) with user's question. Also, it is cost-effective than [LLM Reranker](llm-reranker.md) because it doesn't generate whole passages.&#x20;

## Usage

To initialize an instance of UPRReranker:

```python
from RAGchain.reranker import UPRReranker

# if use gpu
reranker = UPRReranker(use_gpu=True)
```

To rank given set of passages:

```python
query ="What causes global warming?"
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier

reranked_passages= reranker.rerank(query=query, passages=passages)
print(reranked_passages)
```
