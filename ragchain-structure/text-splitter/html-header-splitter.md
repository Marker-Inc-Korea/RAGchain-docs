# HTML Header Text Splitter

## Overview

The `HTMLHeaderSplitter` class in the RAGchain library is a text splitter that splits documents based on HTML headers. 
This class inherits from the `BaseTextSplitter` class and uses the [`HTMLHeaderTextSplitter`](https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/HTML_header_metadata) from the langchain library to perform the splitting.


The difference of `MarkDownHeaderSplitter` is that `HTMLHeaderSplitter` can return chunks element by element or combine elements with the same metadata, 
with the objectives of (a) keeping related text grouped (more or less) semantically and (b) preserving context-rich information encoded in document structures. 
It can be used with other text splitters as part of a chunking pipeline.



## Usage

### Initialization

First, initialize an instance of `HTMLHeaderSplitter`, you can provide the following parameters: <br>
- `headers_to_split_on`: A list of tuples that specify the headers to split the document on. Each tuple consists of an HTML header and a key for metadata.<br>
  Allowed header values are h1, h2, h3, h4, h5, h6.<br>
The default value is `[("h1", "Header 1"), ("h2", "Header 2"), ("h3", "Header 3")]`.
- `return_each_element`: A boolean that specifies whether to return each element with its associated headers. The default value is False.


For example:

```python
from RAGchain.preprocess.text_splitter import HTMLHeaderSplitter

html_header_splitter = HTMLHeaderSplitter()
```

### Split document

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```python
passages = html_header_splitter.split_document(document)
```

# [Limitation](https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/HTML_header_metadata#limitations)
Splitter can't recognize header some cases. Please note above hyperlink!