---
description: MonoT5Reranker Class Documentation
---

# MonoT5 Reranker

## Overview

The `MonoT5Reranker` class is a reranker that uses the MonoT5 model. This model rerank passages based on their relevance to a given query.&#x20;

## Usage

### Initialize

To use the `MonoT5Reranker` class, you first need to create an instance of the class. This is done by calling the class constructor, which can take several optional parameters to customize the behavior of the reranker. If no parameters are provided, the reranker will be initialized with default values.

```python
from RAGchain.reranker import MonoT5Reranker

reranker = MonoT5Reranker()
```

In the test code provided, no parameters are passed to the constructor, which means the reranker will use the default model '[castorini/monot5-3b-msmarco-10k](https://huggingface.co/castorini/monot5-3b-msmarco-10k)'.&#x20;

You can set whether you use Automatic Mixed Precision (AMP) for model inference, or use any specific tokens to represent True or False when encoding the input using additional parameter. You can check out API spec at [here](https://nomadamas.github.io/RAGchain/build/html/RAGchain.reranker.pygaggle.html#RAGchain.reranker.pygaggle.monoT5.MonoT5Reranker).

### Rerank

After the `MonoT5Reranker` instance has been initialized, you can use the `rerank` method to rerank a list of passages based on a given query. The `rerank` method takes two parameters: a query (a string), and a list of passages.

```python
query = "What is query decomposition?"
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier

reranked_passages = reranker.rerank(query, test_passages)
print(reranked_passages)
```

The `rerank` method returns a new list of the passages, reordered based on the MonoT5 model. The length of the reranked list is the same as the original list of passages, and the order of the passages may be different, indicating that the passages have been reranked.
