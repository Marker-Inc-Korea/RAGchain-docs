---
description: BasicRunPipeline Class Documentation
---

# BasicRunPipeline

## Overview

The `BasicRunPipeline` class handles the run process of document question answering. It is simple pipeline for beginners. It retrieves passages from a retrieval module, runs a Language Model (LLM) module to get an answer, and returns the answer and the retrieved passages.

## Usage

### Initialize

The `BasicRunPipeline` class is initialized with the following parameters:

* `retrieval`: Retrieval module to retrieve passages.
* `llm`: LLM module to get answer. If not provided, a default `BasicLLM` module is used.

```python
from RAGchain.pipeline.basic import BasicRunPipeline
from RAGchain.retrieval import BM25Retrieval
from RAGchain.llm.basic import BasicLLM

retrieval = BM25Retrieval(save_path="./bm25.pkl")
llm = BasicLLM(retrieval)
pipeline = BasicRunPipeline(retrieval=retrieval, llm=llm)
```

### Run

The `run` method executes the run pipeline. It takes a `query` string as input and returns a tuple containing the answer and the retrieved passages.

```python
answer, passages = pipeline.run(query="Where is the capital of Korea?")
```

This method will retrieve passages from the retrieval module, run the LLM module to get an answer, and return the answer and the retrieved passages.
