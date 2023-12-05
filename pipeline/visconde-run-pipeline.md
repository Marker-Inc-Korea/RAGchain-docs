# Visconde Pipeline

## Overview

The `ViscondeRunPipeline` class is implementation of Visconde pipeline. You can check out Visconde paper at [here](https://arxiv.org/abs/2212.09656).&#x20;

Visconde pipeline perform three task: decompose, retrieve, and aggregate. It uses [Query Decomposition](../../utils/query-decomposition.md) for answering multi-hop questions. So, it is effective to answer real-world questions  that need to check out multiple passages.

## Usage

#### Initialize

To create an instance of `ViscondeRunPipeline`, you need to provide an instance of a [`Retrieval`](../retrieval/) class, and llm module to generate answer. Optionally, you can specify the instance of [query decomposition module](../utils/query-decomposition.md), a custom prompt, and other options for retrieval and use passage count for generation.
FYI, you can't use chat model for this pipeline.
It has a default prompt for strategyQA style multi-hop questions. You need to change prompt using PromptTemplate if you want to use another few-shot prompts.

```python
from RAGchain.pipeline import ViscondeRunPipeline
from RAGchain.retrieval import BM25Retrieval
from langchain.llms.openai import OpenAI

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path")
pipeline = ViscondeRunPipeline(retrieval, OpenAI(model_name="babbage-002"))
```

#### Ask

You can ask a question to the LLM model and get an answer using `invoke` method. Also, you can use another LCEL's method like stream or batch as well.

```python
question = "Is reranker and retriever have same role?"
answer = pipeline.run.invoke({"question": question})
print(answer)
```

If you want to get used passages or relevance scores of retrieved passages, you can use `get_passages_and_run` method.

```python
answers, passages, scores = pipeline.get_passages_and_run([question])
```
