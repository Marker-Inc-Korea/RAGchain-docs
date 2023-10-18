---
description: HybridRetrieval Class Documentation
---

# Hybrid Retrieval

### Overview

The `HybridRetrieval` class is designed to retrieve passages from multiple retrievals. It combines retrieval scores using either the Reciprocal Rank Fusion (RRF) algorithm or Convex Combination (CC) algorithm. RRF algorithm calculate final similarity scores based on ranking in each retrievals. CC algorithm can caluclate scores with different weights between each retrievals.

### Usage

#### Initialize

To create an instance of the `HybridRetrieval` class, you need to provide a list of Retrieval objects.&#x20;

You can provide p value, which means retrieve passages counts from each retrievals before run rrf or cc algorithm. If p value is small, it might can't get enought passages to reach top\_k value. You should need more p value if your retrievals have huge passages.&#x20;

If you want to use RRF algorithm, you can provide rrf\_k value, which is hyper parameter in rrf algorithm.

If you want to use CC algorith, you can provide a list of weights corresponding to each retrieval method. The weights should sum up to 1.0.

```python
import chromadb
from RAGchain.retrieval import BM25Retrieval, VectorDBRetrieval, HybridRetrieval
from RAGchain.utils.vectorstore import ChromaSlim
from RAGchain.utils.embed import EmbeddingFactory

# initialize various retrievals
chroma = ChromaSlim(
    client=chromadb.PersistentClient(path='your/path/to/chroma'),
    collection_name='your_collection_name',
    embedding_function=EmbeddingFactory('openai').get()
)
bm25_retrieval = BM25Retrieval(save_path='your/path/to/bm25_file.pkl')
vectordb_retrieval = VectorDBRetrieval(chroma)
retrievals = [bm25_retrieval, vectordb_retrieval]

# if you want to use rrf algorithm
hybrid_retrieval_rrf = HybridRetrieval(retrievals, p=100, method='rrf', rrf_k=60)

# if you want to use cc algorithm
weights = [0.6, 0.4]
hybrid_retrieval_cc = HybridRetrieval(retrievals, p=100, method='cc', weights=weights)
```

#### Ingest

Ingest a list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage)s into all retrievals in the hybrid retrieval.

```python
passages = [ ... ] # your list of Passage objects
hybrid_retrieval_cc.ingest(passages)
```

#### Retrieve

Retrieve top-k passages for a given query.

```python
pythonquery = "What is AI?"
top_k_passages = hybrid_retrieval_cc.retrieve(query)
```

#### Retrieve with filter

You can also filter the retrieved passages. Use the `retrieve_with_filter` method and provide the query, top-k value, and a list of content, filepath, or metadata values to filter by.&#x20;

In this method uses `DB.search` method. Please refer [here](https://nomadamas.github.io/RAGchain/build/html/RAGchain.DB.html#RAGchain.DB.base.BaseDB.search) for further information.

Here's an example:

```python
filtered_passages = hybrid_retrieval_cc.retrieve_with_filter(query, top_k, filepath=["filepath1", "filepath3"])
# This code will search top-5 most similar passages with filepath1 and filepath3
```
