---
description: Documentation for Text Splitter Module
---

# Text Spliter

## Overview

The Text Splitter module is an essential component in our framework, designed to handle large volumes of text data. It functions by dividing loaded Document contents into manageable segments, returning a list of Passage objects. This process is essential in the RAG (Retrieval-Augmented Generation) workflow, due to the token limitations imposed by Large Language Models (LLMs).

Given that not all content within a document is useful or relevant for answering questions, it becomes necessary to split documents into smaller passages. These passages can then be analyzed and retrieved more efficiently when providing responses.

Please note that our Text Splitter is not compatible with Langchain's text splitter. We are now implementing all Langchain's text splitters.

## `Document` to `Passage` Conversion
There are many fields in `Passage` schema. You have to set 'source' key in `Document` metadata. It will set to `Passage`'s `filepath` field.

Also, you can set `content_datetime` filed at `Document` metadata. You can use `datetime.datetime` or `str` with `YYYY-MM-DD HH:MM:SS` format.
It will set to `Passage`'s `content_datetime` field.

Plus, you can set `importance` field at `Document` metadata. It will set to `Passage`'s `importance` field.


## Supporting Text Splitter

1. [RecursiveTextSplitter](recursive-text-splitter.md)
2. [markdown-header-splitter](markdown-header-splitter.md)
3. [html-header-splitter](html-header-splitter.md)
4. [Code splitter](code-splitter.md)
5. [Token splitter](token-splitter.md)


## Roles of the Text Splitter in the Framework

The primary role of the Text Splitter module within our framework involves breaking down extensive Document contents into smaller Passage objects. By doing so, it allows us to manage and process vast amounts of data more effectively and efficiently.

In particular, this becomes crucial in contexts such as RAG workflows where LLMs have specific token limits. With these constraints in mind, utilizing all document contents without filtering or splitting could lead to inefficiencies or inaccuracies during information retrieval and question-answering processes.

Moreover, as many documents often contain irrelevant information or 'noise,' splitting these documents into tiny passages aids in isolating and retrieving valuable information pertinent to answering questions accurately and promptly.
