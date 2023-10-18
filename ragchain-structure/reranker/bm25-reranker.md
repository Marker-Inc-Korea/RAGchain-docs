# BM25 Reranker

## Overview

The `BM25Reranker` is a class that leverages the BM25 ranking function to rerank a list of passages based on their relevance to a given query.&#x20;

## Usage

### Initialization

Create an instance of `BM25Reranker`. The `tokenizer_name` parameter should specify the name of the tokenizer to use. If not provided, it defaults to `"gpt2"`. You can put any tokenizer name from huggingface.

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.reranker import BM25Reranker
</strong><strong>
</strong><strong>reranker = BM25Reranker(tokenizer_name="gpt2")
</strong></code></pre>

### Rerank

Call the `rerank` method on your `BM25Reranker` instance to rerank a list of passages. This method takes as input a query string and a list of `Passage` objects, and returns a list of `Passage` objects sorted by their relevance to the query.

```python
query = "What is query decomposition?"
passages = [...list_of_passages...] # Assume we have list_of_passages retreived earlier

rerank_passages = bm25_reranker.rerank(query, test_passages)
print(rerank_passages)
```

In the `rerank` method, the contents of the passages are first tokenized. Then, a `BM25Okapi` instance is created with the tokenized content. The BM25 scores of the tokenized query with respect to each tokenized content are calculated. The passages are then sorted by their scores in descending order.
