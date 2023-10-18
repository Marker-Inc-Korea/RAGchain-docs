---
description: QueryDecomposition Class Documentation
---

# Query Decomposition

## Overview

The `QueryDecomposition` class is used to decompose a multi-hop question into multiple single-hop questions using a LLM model. The class uses a default decomposition prompt from the [Visconde paper](https://arxiv.org/pdf/2212.09656.pdf). And default prompt is derived from few-shot prompts from the strategyQA dataset.

## Usage

### Initialize

To use the `QueryDecomposition` class, you first need to create an instance of the class.

```python
from RAGchain.utils.query_decompose import QueryDecomposition

decomposer = QueryDecomposition()
```

You can put additional parameter `model_name` and `api_base` for using custom model.

### Decompose

After the `QueryDecomposition` instance has been initialized, you can use the `decompose` method to decompose a query into multiple single-hop questions. The `decompose` method takes a query (a string) as input and returns a list of decomposed queries.

```python
query = "Is it legal for a licensed child driving Mercedes-Benz to be employed in US?"
decomposed_queries = decomposer.decompose(query)
print(decomposed_queries)
>>> ["What is the minimum driving age in the US?", "What is the minimum age for someone to be employed in the US?"]
```

If the input query is not multi-hop question, so it doesn't need any decomposition, it returns **empty list**.&#x20;

```python
query = "What is the atomic number of hydrogen?" # it is single-hop question
decomposed_queries = decomposer.decompose(query)
print(len(decomposed_queries))
>>> 0
```
