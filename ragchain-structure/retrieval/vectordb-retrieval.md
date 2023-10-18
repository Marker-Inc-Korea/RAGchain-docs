---
description: VectorDBRetrieval Class Documentation
---

# VectorDB Retrieval

## Overview

The `VectorDBRetrieval` class is a retrieval class that uses VectorDB as a backend. You can use Dense Retrieval with this class easily.

&#x20;It first embeds the passage content using an embedding model, then stores the embedded vector in VectorDB. When retrieving, it embeds the query and searches for the most similar vectors in VectorDB. Lastly, it returns the passages that have the most similar vectors.

## Usage

### Initialize

First, prepare the VectorDB instance you want to use and set up your database. In this example, we are using `Chroma` and [`ChromaSlim`](../../utils/slim-vector-store/chroma-slim.md) as our VectorDB. [`ChromaSlim`](../../utils/slim-vector-store/chroma-slim.md) is VectorStore that stores only passage ID and embedding vectors, which optimizes for RAGchain. The Chroma client requires a path to save the database and an embedding function.

* Using Langchain Chroma VectorStore

```python
from langchain.vectorstores import Chroma
import chromadb
from RAGchain.utils.embed import EmbeddingFactory
from RAGchain.retrieval import VectorDBRetrieval

chroma_path = "path/to/your/chroma"
embedding_function = EmbeddingFactory('openai').get()
client = chromadb.PersistentClient(path=chroma_path)

chroma = Chroma(client=client,
                collection_name='your_collection_name',
                embedding_function=embedding_function)

vectordb_retrieval = VectorDBRetrieval(vectordb=chroma)
```

* Using RAGchain SlimVectorStore

```python
from RAGchain.utils.vectorstore import ChromaSlim
import chromadb
from RAGchain.utils.embed import EmbeddingFactory
from RAGchain.retrieval import VectorDBRetrieval

chroma_path = "path/to/your/chroma"
embedding_function = EmbeddingFactory('openai').get()
client = chromadb.PersistentClient(path=chroma_path)

chroma = ChromaSlim(client=client,
                    collection_name='your_collection_name',
                    embedding_function=embedding_function)

slim_vectordb_retrieval = VectorDBRetrieval(vectordb=chroma)
```

### Ingest

Ingest a list of passages into your retrieval system.

```python
passages = [...] # your list of passages here
slim_vectordb_retrieval.ingest(passages)
```

### Retrieve

Retrieve top-k passages for a given query.

```python
query = "What's the main advantage of using Slim Vector store?"
top_k_passages = slim_vectordb_retrieval.retrieve(query=query, top_k=5)
```

### Retrieve with filter

You can also filter the retrieved passages. Use the `retrieve_with_filter` method and provide the query, top-k value, and a list of content, filepath, or metadata values to filter by.&#x20;

In this method uses `DB.search` method. Please refer [here](https://nomadamas.github.io/RAGchain/build/html/RAGchain.DB.html#RAGchain.DB.base.BaseDB.search) for further information.

Here's an example:

```python
filtered_passages = slim_vectordb_retrieval.retrieve_with_filter(query, top_k, filepath=["filepath1", "filepath3"])
# This code will search top-5 most similar passages with filepath1 and filepath3
```
