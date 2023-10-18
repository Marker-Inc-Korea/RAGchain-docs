---
description: LLMReranker Class Documentation
---

# LLM Reranker

## Overview

The `LLMReranker` class is a reranker based on LLM model itself. In LLMReranker, LLM models sort retrieved passages with zero-shot prompt. In this way, you can get high quality reranked passages with direct and semantic connection with user's question.

## Usage

### Initialize

To use the `LLMReranker` class, you first need to create an instance of the class. You can set model\_name and model's api base url with additional parameter.

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.reranker import LLMReranker
</strong><strong>
</strong><strong>reranker = LLMReranker()
</strong></code></pre>

### Rerank

After the `LLMReranker` instance has been initialized, you can use the `rerank` method to rerank a list of passages based on a given query. The `rerank` method takes two parameters: a query (a string), and a list of passages.

```python
query = "What is query decomposition?"
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier

reranked_passages = reranker.rerank(query, test_passages)
print(reranked_passages)
```

The `rerank` method returns a new list of the passages, reordered based on the LLM reranking.

### Sliding Window Rerank

When using LLM as reranker, you can face max token error because it consumes lots of tokens for reranking. In this case, you can't rerank all passages in one time. So, `LLMReranker` supports sliding window rerank. It slices passages to window-size passages, and rerank with small amount of passages per one time. In this way, you can rerank all passages without max token error.

However, it has limits that you can't rerank all passages completely. So, you need to rerank again to get complete reranked passages.&#x20;

To use sliding window reranking, you simply use `rerank_sliding_window()` method with window\_size parameter.&#x20;

```python
query = "What is query decomposition?"
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier

reranked_passages = reranker.rerank_sliding_window(query, test_passages, window_size=5)
print(reranked_passages)
```
