---
description: ChromaSlim Class Documentation
---

# Chroma Slim

## Overview

The `ChromaSlim` class is a slim vector store of [Chroma](https://docs.trychroma.com/), optimized for RAGchain.

## Usage

Its usage is similar to Langchain's [`Chroma`](https://python.langchain.com/docs/integrations/vectorstores/chroma) class. Due to its inheritance to [`Chroma`](https://python.langchain.com/docs/integrations/vectorstores/chroma) class, you can use any function in [`Chroma`](https://python.langchain.com/docs/integrations/vectorstores/chroma) class. Plus, you can initialize with [`Chroma`](https://python.langchain.com/docs/integrations/vectorstores/chroma) class initializer.

For the optimal utilization of `ChromaSlim` VectorStore, developers are strongly recommended to employ the `add_passages()` method when saving passages. The use of alternative methods may not fully leverage the capabilities and advantages inherent in Slim VectorStore.

Here is a basic example:

```python
import chromadb
from RAGchain.utils.vectorstore import ChromaSlim
from RAGchain.utils.embed import EmbeddingFactory

chroma_path = "your/chroma/path"
chroma_slim = ChromaSlim(
    client=chromadb.PersistentClient(path=chroma_path),
    collection_name="your-chroma-collection",
    embedding_function=EmbeddingFactory('openai').get()
)

# add passage to ChromaSlim
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier
chroma_slim.add_passages(passages)
```
