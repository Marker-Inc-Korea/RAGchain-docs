---
description: Retrieval Module Documentation
---

# Retrieval

## Overview

With Retrieval module, you can ingest passage contents to vector representations. Then the module can retrieve the most similar passages for answering to given questions.

## Supporting Retrievals

#### 1. [BM25 Retrieval](bm25-retrieval.md)

BM25 is a bag-of-words retrieval function that ranks a set of documents based on the query terms appearing in each document. It uses term frequency (TF) and inverse document frequency (IDF) to calculate a weight for each word in a document.

#### 2. [Hybrid Retrieval](hybrid-retrieval.md)

Hybrid Retrieval combines multiple retrieval methods into one system. It allows you to leverage the strengths of multiple methods at once, potentially leading to better results than using any single method alone.

#### 3. [Hyde Retrieval](hyde-retrieval.md)

Hyde is a passage retrieval method that generates hypothetical passages using language models and retrieves passages based on that generated passages.

#### 4. [VectorDB Retrieval](vectordb-retrieval.md)

VectorDBRetrieval uses VectorDB as a backend for storing embedded vectors of passages and retrieving similar vectors given an input query using similarity search.

## Role of the Retrievals in RAGchain

The role of these retrievals within our framework is essential as they serve as the backbone for information extraction from large amounts of data or documents based on user queries or needs. They provide efficient ways to search through data by embedding or ranking information so that relevant results can be returned quickly even with massive amounts of data.

## Advantages of Retrievals

Each type of retrieval system offers its own unique advantages:

* **BM25**: This method is simple yet effective, especially when dealing with unstructured text data where term frequency can indicate relevance.
* **Hybrid**: By combining multiple methods, this approach can take advantage of their individual strengths while mitigating their weaknesses.
* **Hyde**: This method's use of hypotheticals allows it to perform more precise search.&#x20;
* **VectorDB**: The use of vector embeddings enables this method to capture semantic relationships between words and phrases beyond simple keyword matching.

Remember that no single method will be best for all tasks; you should choose your retrieval system based on your specific needs and constraints.

\
