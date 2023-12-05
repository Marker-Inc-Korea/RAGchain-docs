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
retrieval = BM25Retrieval(save_path="./bm25.pkl")
pipeline = BasicRunPipeline(retrieval=retrieval, llm=OpenAI())
```

### Run

The `run` variable is runnable of Langchain LCEL. So you can use all method for running pipeline, like `invoke`, `stream`, `batch`, and so on.

```python
answer = pipeline.run.invoke({"question": "Where is the capital of Korea?"})
```

If you want to get used passages or relevance scores of retrieved passages, you can use `get_passages_and_run` method.

```python
answers, passages, scores = pipeline.get_passages_and_run(["Where is the capital of Korea?"])
```
