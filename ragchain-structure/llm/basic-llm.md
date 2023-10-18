---
description: BasicLLM Class Documentation
---

# Basic LLM

## Overview

The `BasicLLM` class is the simplest LLM module for question answering with retrieved passages. You can easily starts RAGchain with this `BasicLLM` module. It supports stream and chat history features by default.

## Usage

#### Initialize

To create an instance of `BasicLLM`, you need to provide an instance of a [`Retrieval`](../retrieval/) class. Optionally, you can specify the [name of the LLM model](./#use-custom-llm), the base URL of the LLM API endpoint, a [custom prompt](./#use-custom-prompt) function and a [streaming](./#stream-answers) function.

```python
from RAGchain.llm.basic import BasicLLM
from RAGchain.retrieval import BM25Retrieval

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path")
llm = BasicLLM(retrieval=retrieval)
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `ask` method.

```python
question = "What is AI?"
answer, passages = llm.ask(question)
print(answer)
```

\
