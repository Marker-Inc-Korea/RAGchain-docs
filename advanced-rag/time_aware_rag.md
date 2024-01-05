---
description: Time-Aware RAG
---

# Time-Aware RAG
In real-world applications, you'll often find that the latest information is more valuable than outdated data.
However, manually discarding old information can be challenging and potentially harmful, as this information might be useful for other queries.
Therefore, time-aware RAG is crucial for certain applications.

Here, we introduce some useful tools for time-aware RAG. 

## `Passage` content_datetime

First, we have `content_datetime` in `Passage` schema, available from v0.2.3.
This field is automatically filled with the datetime that `Passage` is created, or you can manually set it.
When you edit this passage, the `content_datetime` will be updated to the current datetime.
You can use this field for time-aware RAG.


## SimpleTimeReranker

This is the simplest way to implement time-aware RAG.
After retrieving passages, you can sort them by `content_datetime`.

```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passages = retrieval.retreive(query)

# rerank passages by content_datetime
reranker = SimpleTimeReranker()
reranked_passages = reranker.rerank(passages)

```

FYI, you don't have to input any query to `rerank` method, because `SimpleTimeReranker` doesn't inherit from `BaseReranker` class.


## WeightedTimeReranker
If you want to mix `content_datetime` with relevance scores, you can use `WeightedTimeReranker`.
It is similar with Langchain's [`TimeWeightedVectorStoreRetriever`](https://python.langchain.com/docs/modules/data_connection/retrievers/time_weighted_vectorstore), but you can use `WeightedTimeReranker` with any retrievals in RAGchain.

So, the algorithm to rerank passages is as follows:
```
relavnace_score + (1.0 - decay_rate) ^ hours_passed
```
In this algorithm, relevance_score is normalized.

You can easily use `WeightedTimeReranker` as follows:
```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passage_ids, scores = retrieval.retreive_id_with_scores(query)
passages = retrieval.fetch_date(passage_ids)

# rerank passages by content_datetime
reranker = WeightedTimeReranker(decay_rate=0.02)
reranked_passages = reranker.rerank(passages, scores)

```


## Set a Hard Limit of Passage datetime

Another simply, yet powerful way to implement time-aware RAG is to set a hard limit of passage `content_datetime`.
You can achieve this by using `retrieve_with_filter` at any [`Retrieval`](/ragchain-structure/retrieval/README.md) class you can use.
You can set multiple time ranges at once, then it only retrieves passages in the time ranges.

```python
from datetime import datetime

query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passages = retrieval.retrieve_with_filter(query, content_datetime_range=[
    (datetime(2021, 1, 1), datetime(2021, 1, 31)),
]) # only retrieve passages in January 2021

```


## ClusterTimeCompressor

If you want to use recent information, but keep old and unique information, you can use `ClusterTimeCompressor`.
This class semantically clusters passages, and keep only latest passage in each cluster.
For clustering passages, it uses [`SemanticClustering`](../utils/semantic-clustering.md).

You can select `split_by_sentences` option when initializing `ClusterTimeCompressor`. If this option is True, it splits passages to each sentence and clusters them.
This option can be helpful that each passage size is big or contain whole different meanings in one passage.

```python
query = "What is the capital of Korea?"
retrieval = BM25Retrieval('/path/to/your/bm25.pkl')
passages = retrieval.retreive(query, top_k=50)

compressor = ClusterTimeCompressor(SemanticClustering(EmbeddingFactory('openai').get(), 'kmeans'), split_by_sentences=True)
compressed_passages = compressor.compress(passages)
```
