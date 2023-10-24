---
description: Documentation for Text Splitter Module
---

# Text Spliter

## Overview

The Text Splitter module is a essential component in our framework, designed to handle large volumes of text data. It functions by dividing loaded Document contents into manageable segments, returning a list of Passage objects. This process is essential in the RAG (Retrieval-Augmented Generation) workflow, due to the token limitations imposed by Large Language Models (LLMs).

Given that not all content within a document is useful or relevant for answering questions, it becomes necessary to split documents into smaller passages. These passages can then be analyzed and retrieved more efficiently when providing responses.

Please note that our Text Splitter is not compatible with Langchain's text splitter. We are now implementing all Langchain's text splitters.

## Supporting Text Splitter

1. [RecursiveTextSplitter](recursive-text-splitter.md) :&#x20;
2. [markdown-header-text-splitter](markdown-header-text-splitter.md)
3. [html-header-text-splitter](html-header-text-splitter.md)

More text splitters are coming soon! ([related issue](https://github.com/NomaDamas/RAGchain/issues/255))

## Roles of the Text Splitter in the Framework

The primary role of the Text Splitter module within our framework involves breaking down extensive Document contents into smaller Passage objects. By doing so, it allows us to manage and process vast amounts of data more effectively and efficiently.

In particular, this becomes crucial in contexts such as RAG workflows where LLMs have specific token limits. With these constraints in mind, utilizing all document contents without filtering or splitting could lead to inefficiencies or inaccuracies during information retrieval and question-answering processes.

Moreover, as many documents often contain irrelevant information or 'noise,' splitting these documents into tiny passages aids in isolating and retrieving valuable information pertinent to answering questions accurately and promptly.
