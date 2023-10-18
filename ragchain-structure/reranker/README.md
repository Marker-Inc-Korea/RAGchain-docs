# Reranker

## Overview

The reranker is a part of the retrieval process in information retrieval systems. It's a system that reorders the list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage)s initially retrieved by a base retrieval model, usually with the goal of improving precision at top ranks. This approach is particularly useful when dealing with large document collections where exhaustive computation for all documents is not feasible or efficient.

## Supporting Reranker

### 1. UPR reranker

It uses a language model to generate a question based on the passage and reranks the passages by the likelihood of the question.&#x20;

### 2. TART reranker

It is designed to rerank passages using specific instructions.&#x20;

### 3. MonoT5 reranker

The `MonoT5Reranker` class is a reranker that uses the MonoT5 model. This model rerank passages based on their relevance to a given query.&#x20;

### 4. LLM reranker

LLM uses pre-trained language models like GPT or Llama can be used to rank passages based on their likelihood of being relevant to user queries.

### 5. BM25 reranker

The `BM25Reranker` is a class that leverages the BM25 ranking function to rerank a list of passages based on their relevance to a given query.&#x20;

## Roles of the Reranker in the Framework

The primary role of a reranker in RAGchain:

1. **Improving Precision**: By reordering retrieved results using more sophisticated models than initial retrieval mechanisms.
2. **Diversity**: By providing an opportunity to introduce diversity into search results by using different ranking algorithms.
3. **Scalability**: When dealing with large-scale data sets, it might not be feasible to apply complex machine learning algorithms on all data points due to computational limitations.

## Advantages of Using A Reranker

1. **Improved Performance**: Re-ranking can often improve performance over using single retrieval alone.
2. **Ensemble Learning Benefits**: Combining different types/models can lead to better generalization and improved performance.
3. **Computational Efficiency**: Instead of applying expensive computations across all data points initially retrieved, rerankers focus on top-k results which saves resources while still improving accuracy.
