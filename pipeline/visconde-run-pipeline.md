# Visconde Pipeline

## Overview

The `ViscondeRunPipeline` class is implementation of Visconde pipeline. You can check out Visconde paper at [here](https://arxiv.org/abs/2212.09656).&#x20;

Visconde pipeline perform three task: decompose, retrieve, and aggregate. It uses [Query Decomposition](../../utils/query-decomposition.md) for answering multi-hop questions. So, it is effective to answer real-world questions  that need to check out multiple passages.

## Usage

#### Initialize

To create an instance of `ViscondeRunPipeline`, you need to provide an instance of a [`Retrieval`](../retrieval/) class. Optionally, you can specify the [name of the LLM model for decomposition](../utils/query-decomposition.md), a custom system prompt, and other options for [`CompletionLLM`](../ragchain-structure/llm/completion-llm.md)
It has a default prompt for strategyQA style multi-hop questions. You need to change prompt using prompt_func if you want to use another few-shot prompts.

```python
from RAGchain.pipeline import ViscondeRunPipeline
from RAGchain.retrieval import BM25Retrieval

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path")
pipeline = ViscondeRunPipeline(retrieval)
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `run` method.

```python
question = "Is reranker and retriever have same role?"
answer, passages = pipeline.run(question)
print(answer)
```
