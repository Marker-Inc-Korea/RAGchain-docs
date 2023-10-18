---
description: BasicIngestPipeline Class Documentation
---

# BasicIngestPipeline

## Overview

The `BasicIngestPipeline` class handles the ingestion process of documents into a DB and a retrieval system. It is simple pipeline for beginners. It loads files from a directory using a file loader, splits the document into passages using a text splitter, saves the passages to a database, and ingests the passages into a retrieval module.

## Usage

### Initialize

The `BasicIngestPipeline` class is initialized with the following parameters:

* [`file_loader`](../ragchain-structure/file-loader/) : File loader to load documents. You can use any file loader from Langchain and RAGchain.
* [`db`](../ragchain-structure/db/): Database to save passages.
* [`retrieval`](../ragchain-structure/retrieval/): Retrieval module to ingest passages.
* [`text_splitter`](../ragchain-structure/text-spliter/): Text splitter to split document into passages. Default is [`RecursiveTextSplitter`](../ragchain-structure/text-spliter/recursive-text-splitter.md).
* `ignore_existed_file`: If True, ignore existed file in database. Default is True. It uses [`FileCache`](../utils/file-cache.md) internally.

```python
from RAGchain.pipeline.basic import BasicIngestPipeline
from RAGchain.DB import PickleDB
from RAGchain.retrieval import BM25Retrieval
from RAGchain.preprocess.loader import FileLoader

file_loader = FileLoader(target_dir="your/path/to/file/dir")
db = PickleDB("your/path/to/pickle.pkl")
retrieval = BM25Retrieval(save_path="your/path/to/bm25.pkl")
pipeline = BasicIngestPipeline(file_loader=file_loader, db=db, retrieval=retrieval)
```

### Run

The `run` method executes the ingest pipeline. It takes an optional `target_dir` parameter, which specifies the target directory to load documents from. If `target_dir` is not provided, it uses the `target_dir` from the file loader that was passed in during the initialization of the pipeline.

```python
pipeline.run()
```

This method will load the documents, split them into passages, save the passages to the database, and ingest the passages into the retrieval module.
