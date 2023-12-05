# Rerank Pipeline

### Overview

The `RerankRunPipeline` class is made for using reranker easily. To use this class, you can use [`Reranker`](../reranker/) easily without extra work. For further information about reranker, please check out Reranker documentation.

In this pipeline, first retrieval retrieves passages. Then reranker reranks retrieved passages. Finally, put retrieved passages to LLM model.&#x20;

## Usage

#### Initialize

To create an instance of `RerankRunPipeline`, you need to provide an instance of a [`Retrieval`](../retrieval/) class and [`Reranker`](../reranker/) class. Optionally, you can specify which [LLM](../ragchain-structure/llm/README.md) model you want to use.

```python
from RAGchain.pipeline import RerankRunPipeline
from RAGchain.retrieval import BM25Retrieval
from RAGchain.reranker import MonoT5Reranker

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path") 
reranker = MonoT5Reranker()
pipeline = RerankRunPipeline(retrieval=retrieval, reranker=reranker, llm=OpenAI()) 
```

#### Run Pipeline

The `run` variable is runnable of Langchain LCEL. So you can use all method for running pipeline, like `invoke`, `stream`, `batch`, and so on.

```python
answer = pipeline.run.invoke({"question": "Where is the capital of Korea?"})
```

If you want to get used passages or relevance scores of retrieved passages, you can use `get_passages_and_run` method.

```python
answers, passages, scores = pipeline.get_passages_and_run(["Where is the capital of Korea?"])
```
