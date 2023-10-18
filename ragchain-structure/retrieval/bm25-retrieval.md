---
description: BM25Retrieval Class Documentation
---

# BM25 Retrieval

## Overview

The `BM25Retrieval` class is used for BM25 retrieval. BM25 is the most popular TF-IDF method for retrieval, which reflects how important a word is to a document. It is often called sparse retrieval. It is different with dense retrieval, which is using embedding model and similarity search. Dense retrieval search passage using semantic similarity, but sparse retrieval uses word counts. If you use documents in specific domains, `BM25Retrieval` can be more useful than `VectorDBRetrieval`.

&#x20;It uses the BM25Okapi algorithm for scoring and ranking the passages. There will be extra algorithm for `BM25Retrieval` ([relevant issue](https://github.com/NomaDamas/RAGchain/issues/209)).



## Usage

#### Initialize

To create an instance of the `BM25Retrieval` class, you need to provide the path to the saved BM25 data. The data should be in either `.pkl` or `.pickle` format.&#x20;

You can also specify the name of the tokenizer to be used (optional). As default, [gpt tokenizer](https://huggingface.co/gpt2) will be used.

Here's an example of initializing the `BM25Retrieval` object:

```python
bm25_path = "path/to/bm25_retrieval.pkl" 
bm25_retrieval = BM25Retrieval(save_path=bm25_path)
```

Please make sure to replace `"path/to/bm25_retrieval.pkl"` with the actual path where you want to save the BM25 retrieval data.

#### Ingest

Before you can retrieve passages, you need to ingest them into the BM25Retrieval object. Passages should be provided as a list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects.&#x20;

Here's an example of ingesting passages:

```python
passages = [
    Passage(id="passage_id_1", content="This is the first passage.", filepath="filepath"),
    Passage(id="passage_id_2", content="This is the second passage.", filepath="filepath"),
    Passage(id="passage_id_3", content="This is the third passage.", filepath="filepath")
]
bm25_retrieval.ingest(passages)
```

#### Retrieve

To retrieve relevant passages based on a query, use the `retrieve` method. You can specify the query and the number of top-k passages to retrieve. \
Here's an example:

```python
query = "Test query?" # replace with your query 
top_k = 5
retrieved_passages = bm25_retrieval.retrieve(query, top_k)
```

#### Retrieve with filter

You can also filter the retrieved passages. Use the `retrieve_with_filter` method and provide the query, top-k value, and a list of content, filepath, or metadata values to filter by.&#x20;

In this method uses `DB.search` method. Please refer [here](https://nomadamas.github.io/RAGchain/build/html/RAGchain.DB.html#RAGchain.DB.base.BaseDB.search) for further information.

Here's an example:

```python
filtered_passages = bm25_retrieval.retrieve_with_filter(query, top_k, filepath=["filepath1", "filepath3"])
# This code will search top-5 most similar passages with filepath1 and filepath3
```

\
\
