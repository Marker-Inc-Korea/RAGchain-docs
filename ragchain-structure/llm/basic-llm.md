---
description: BasicLLM Class Documentation
---

# Basic LLM

## Overview

The `BasicLLM` class is the simplest LLM module for question answering with retrieved passages. You can easily start RAGchain with this `BasicLLM` module. It supports stream and chat history features by default.

## Usage

#### Initialize

While creating an instance of `BasicLLM`, you can specify the [name of the LLM model](./#use-custom-llm), the base URL of the LLM API endpoint, a [custom prompt](./#use-custom-prompt) function and a [streaming](./#stream-answers) function.

```python
from RAGchain.llm import BasicLLM

llm = BasicLLM()
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `ask` method. You have to provide retrieved passages as input.

```python
question = "What is AI?"
passages = [<your passages>]

answer, passages = llm.ask(question)
print(answer)
```
