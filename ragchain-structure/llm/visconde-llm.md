# Visconde LLM

## Overview

The `ViscondeLLM` class is implementation of Visconde pipeline. You can check out Visconde paper at [here](https://arxiv.org/abs/2212.09656).&#x20;

Visconde pipeline perform three task: decompose, retrieve, and aggregate. It uses [Query Decomposition](../../utils/query-decomposition.md) for answering multi-hop questions. So, it is effective to answer real-world questions  that need to check out multiple passages.

## Usage

#### Initialize

To create an instance of `ViscondeLLM`, you need to provide an instance of a [`Retrieval`](../retrieval/) class. Optionally, you can specify the [name of the LLM model](./#use-custom-llm), the base URL of the LLM API endpoint, the name of the LLM model for query decomposition, a custom system prompt and a [streaming](./#stream-answers) function.

```python
from RAGchain.llm.visconde import ViscondeLLM
from RAGchain.retrieval import BM25Retrieval

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path")
llm = ViscondeLLM(retrieval=retrieval)
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `ask` method.

```python
question = "What is AI and how can I develop that?"
answer, passages = llm.ask(question)
print(answer)
```

\
