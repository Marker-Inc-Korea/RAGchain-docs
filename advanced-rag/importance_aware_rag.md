---
description: Importance-Aware RAG
---

# Importance-Aware RAG
In some cases, you may want to prioritize certain passages over others.
For example, when you try to find specific information at Google search, there are some websites that you trust more
than others.
Or, some websites that you don't want to see.
In this case, you can use importance-aware RAG.

Here, we introduce some useful tools for importance-aware RAG.

## `Passage` importance

Importance-RAG can set passage importance by using `Passage`'s `importance` field. 
The default value of `importance` is 0, and you can set this value to any int value.
If it is minus value, its passage is less important than default passages. 
If it is plus value, its passage is more important than default passages.
Using this field, you can retrieve passages with document importance.


## SimpleImportanceReranker
This is the simplest way to implement importance-aware RAG.
After retrieving passages, you can sort them by `importance`.

```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passages = retrieval.retreive(query)

# rerank passages by importance
reranker = SimpleImportanceReranker()
reranked_passages = reranker.rerank(passages)

```

FYI, you don't have to input any query to `rerank` method, because `SimpleImportanceReranker` doesn't inherit from `BaseReranker` class.


## WeightedImportanceReranker
If you want to mix `importance` with relevance scores, you can use `WeightedImportanceReranker`.
It is similar with [`WeightedTimeReranker`](./time_aware_rag.md#WeightedTimeReranker).

The algorithm to rerank passages is as follows:
```
importance_wieght * importance + (1 - importance_weight) * relevance_score
```

You can easily use `WeightedImportanceReranker` as follows:
```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passage_ids, scores = retrieval.retreive_id_with_scores(query)
passages = retrieval.fetch_date(passage_ids)

# rerank passages by importance
reranker = WeightedImportanceReranker(importance_weight=0.5)
reranked_passages = reranker.rerank(passages, scores)

```

## Set a Hard Limit of Passage importance

Another simply, yet powerful way to implement importance-aware RAG is to set a hard limit of passage `importance`.
You can achieve this by using `retrieve_with_filter` at any [`Retrieval`](/ragchain-structure/retrieval/README.md) class you can use.
You can set importance values you want to retrieve.

```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passages = retrieval.retrieve_with_filter(query, importance=[0, 1, 2]) # only retrieve passages with importance 0 ~ 2
```
