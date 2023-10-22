# Markdown Header Text Splitter

## Overview

The `MarkDownHeaderSplitter` is used to split a document into passages based document's header information which a list of separators contain.
The most feature is similar with Langchain's [`MarkdownHeaderTextSplitter`](https://python.langchain.com/docs/modules/data\_connection/document\_transformers/text\_splitters/recursive\_text\_splitter).
It split based on header. <br>

`metadata_etc` of `Passage` contains header information and original document information. 
`metadata_etc` updates new header is two case. <br>
First, whenever new header appear at document, `metadata_etc` is appended new header information.<br>
Second, when a header with an equivalent relationship appears, the metadata is initialized and the newly appeared header is included in the metadata.

## Usage

### Initialization

First, initialize an instance of `MarkDownHeaderSplitter`. For example:

```python
from RAGchain.preprocess.text_splitter import MarkDownHeaderSplitter

splitter = MarkDownHeaderSplitter()
```

### Split document

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```python
passages = splitter.split_document(document)
```
