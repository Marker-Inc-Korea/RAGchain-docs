# RAGchain Structure

This document will guide you through the fundamental structure of RAGchain, helping you understand its core modules and how they interact to provide a high-quality RAG workflows for your needs.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Simple Description structure of RAGchain</p></figcaption></figure>

## Overview

RAGchain is built upon several key modules that serve as the building blocks for creating your own custom RAG workflow. These modules include:

1. **File Loader**
2. **Text Splitter**
3. **Retrieval Module**
4. **DB**
5. **LLM**
6. **Reranker**

Let's explore each module in more detail.

### [File Loader](file-loader/)

The first step in RAG workflow is data ingestion. `File Loader` module reads files containing text data. RAGchain `File Loader` modules provide full compatibility with Langchain's Document Loader, plus special OCR loaders and more.

### [Text Splitter](text-spliter/)

Once the files are loaded, we need to divide longer documents into shorter passages due to context limitations of Large Language Models (LLMs). This process is essential because LLMs can forget contexts in lengthy documents when generating responses or conducting analysis.

The `Text Splitter` module takes care of breaking down long documents into manageable chunks without losing crucial context or meaning from the original content.

### [Retrieval](retrieval/)

After splitting texts into passages, these contents must be converted into vector representations suitable for searching related passages based on user queries. The `Retrieval` module handles both these tasks: transforming document contents into vectors and retrieving relevant passages based on user questions.

### [DB](db/)

To simplify working with multiple retrievals and databases simultaneously, we use `DB` and [`Linker`](../utils/linker.md). In RAGchain, all passage contents and metadata must store in `DB`. And `Linker` is a utility that automatically connects multiple retrieval instances with their respective DBs. With `Linker`, managing multiple retrievals becomes really easy task.

### [LLM](llm/)

Finally comes the `LLM` module - it uses retrieved passages as input to answer user queries. Tjhe `LLM` module also supports stream, custom prompt, custom models, and chat history for your use cases.

### [Reranker](./#reranker)

Reranker re-ranks retrieved passages for higher accuracy and great quality of LLM answers. It is really common using rerankers at RAG workflows, because its boost of performance is quite impressive.&#x20;



You can explore all modules in this docs. You can select what module that you want to use, and quickly build your own RAG workflow for your new service!&#x20;
