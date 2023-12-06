---
description: Build powerful RAG workflows with LLM, compatible with Langchain.
---

# Introduction

**RAGchain** is a framework for developing advanced RAG(Retrieval Augmented Generation) workflow powered by LLM (Large Language Model). \
While existing frameworks like Langchain or LlamaIndex allow you to build simple RAG workflows, they have limitations when it comes to building complex and high-accuracy RAG workflows.

**RAGchain** is designed to overcome these limitations by providing powerful features for **building advanced RAG workflow** easily. Also, it is partially **compatible with Langchain**, allowing you to leverage many of its integrations for vector storage, embeddings, and document loaders.

## Why RAGchain?

RAGchain offers several powerful features for building high-quality RAG workflows:

### **OCR Loaders**

Simple file loaders may not be sufficient when trying to enhance accuracy or ingest real-world documents. OCR models can scan documents and convert them into text with high accuracy, improving the quality of responses from LLMs.

### **Reranker**

Reranking is a popular method used in many research projects to improve retrieval accuracy in RAG workflows. Unlike LangChain, which doesn't include reranking as a default feature, RAGChain comes with various rerankers.

### **Great to use multiple retrievers**

In real-world scenarios, you may need multiple retrievers depending on your requirements. RAGchain is highly optimized for using multiple retrievers. It divides retrieval and DB. [`Retrieval`](ragchain-structure/retrieval/README.md) saves vector representation of contents, and [`DB`](ragchain-structure/db/README.md) saves contents. We connect both with Linker, so it is really easy to use multiple retrievers and DBs.

### **pre-made RAG pipelines**

We provide pre-made pipelines that let you quickly set up RAG workflow. We are planning to make much complex pipelines, which hard to make but powerful. With pipelines, you can build really powerful RAG system quickly and easily.

### Easy benchmarking

It is crucial to benchmark and test your RAG workflows. We have easy benchmarking module for evaluation. Support your own questions and various datasets.

## Compatibility with Langchain

You can use [Document Loaders](https://integrations.langchain.com/), [Vector Stores](https://integrations.langchain.com/vectorstores), [Embedding Models](https://integrations.langchain.com/embeddings), [LLM Models](https://integrations.langchain.com/llms) at RAGchain. Three of them are compatible with RAGchain. Don't worry about lack of integrations that new framework is commonly suffered.&#x20;

Langchain's speciality is amount of integrations they made. RAGchain uses that power, and focus on only RAG system quality and efficiency.&#x20;

## Resources

You can start our framework with [Quick Start](utils/query-decomposition.md#usage).

And check out our [API documentation](https://nomadamas.github.io/RAGchain/build/html/index.html) if you need to find out more about RAGchain.

Plus, feel free to visit our [github repo](https://github.com/NomaDamas/RAGchain) and contribute!&#x20;
