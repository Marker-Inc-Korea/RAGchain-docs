# Recursive Text Splitter

## Overview

The `RecursiveTextSplitter` is used to split a document into passages by recursively splitting on a list of separators. The class also allows for specifying a window size and overlap size to split the document into overlapping passages.&#x20;

The most feature is similar with Langchain's [`RecursiveCharacterTextSplitter`](https://python.langchain.com/docs/modules/data\_connection/document\_transformers/text\_splitters/recursive\_text\_splitter).

## Usage

### Initialization

First, initialize an instance of `RecursiveTextSplitter`. For example:

```python
from RAGchain.preprocess.text_splitter import RecursiveTextSplitter

splitter = RecursiveTextSplitter(chunk_size=500, chunk_overlap=50)
```

### Split document

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```python
passages = splitter.split_document(document)
```
