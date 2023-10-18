# Slim Vector Store

## Overview

Slim Vector Store is vector store class designed for RAGchain. At default, Langchain's [Vector Store](https://python.langchain.com/docs/integrations/vectorstores) is fully compatible with RAGchain. But, it is inefficient because it stores all string contents at every vector store. Because of this limitation, you have to spend lots of storage space when using multiple retrievals.&#x20;

RAGchain store vector representation using retrievals, and store string contents to independent DB. So, you don't have to store string contents to vector store.&#x20;

Using Slim Vector Store, it only stores vector representation and passage ids. It will save a lot of storage when you use multiple retrievals.&#x20;

## Supporting Vector Stores

We are implementing many vector stores, but many vector stores are not implemented yet. When you have to use another vector stores, please find it at Langchain's Vector Store. It is fully compatible with RAGchain.

* [Chroma](chroma-slim.md)
* [Pincone](pinecone-slim.md)
