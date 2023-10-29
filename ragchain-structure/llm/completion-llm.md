---
description: CompletionLLM Class Documentation
---

# Completion LLM

## Overview

The `CompletionLLM` class is the LLM module for question answering with retrieved passages using **completion models**, not chat models.
It supports stream and custom prompt features by default. But, it does not support chat history, because it doesn't use chat models.

## Usage

#### Initialize

While creating an instance of `CompletionLLM`, you can specify the [name of the LLM model](./#use-custom-llm), the base URL of the LLM API endpoint, a [custom prompt](./#use-custom-prompt) function and a [streaming](./#stream-answers) function.

```python
from RAGchain.llm import CompletionLLM

llm = CompletionLLM()
```

#### Ask

You can ask a question to the LLM model and get an answer using `ask` method. You have to provide retrieved passages as input.

```python
question = "What is AI?"
passages = [<your passages>]
answer, passages = llm.ask(question, passages)
print(answer)
```
