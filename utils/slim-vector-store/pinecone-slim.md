---
description: PineconeSlim Class Documentation
---

# Pinecone Slim

## Overview

The `PineconeSlim` class is a slim vector store of [Pinecone](https://www.pinecone.io/), optimized for RAGchain.

## Usage

Its usage is similar to Langchain's [`Pinecone`](https://python.langchain.com/docs/integrations/vectorstores/pinecone) class. Due to its inheritance to [`Pinecone`](https://python.langchain.com/docs/integrations/vectorstores/pinecone) class, you can use any function in [`Pinecone`](https://python.langchain.com/docs/integrations/vectorstores/pinecone) class. Plus, you can initialize with [`Pinecone`](https://python.langchain.com/docs/integrations/vectorstores/pinecone) class initializer.

For the optimal utilization of `PineconeSlim` VectorStore, developers are strongly recommended to employ the `add_passages()` method when saving passages. The use of alternative methods may not fully leverage the capabilities and advantages inherent in Slim VectorStore.

Here is a basic example:

```python
import pinecone
from RAGchain.utils.vectorstore import PineconeSlim
from RAGchain.utils.embed import EmbeddingFactory

index = pinecone.Index(index_name="your_index_name")

# Initialize PineconeSlim
pinecone_slim = PineconeSlim(
    index=index,
    embedding=EmbeddingFactory('openai').get(),
    text_key="text",
    namespace="your_namespace"
)

# add passage to PineconeSlim
passages =[...list_of_passages...] # Assume we have list_of_passages retrieved earlier
pinecone_slim.add_passages(passages)
```
