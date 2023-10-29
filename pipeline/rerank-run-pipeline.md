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
pipeline = RerankRunPipeline(retrieval=retrieval, reranker=reranker) 
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `run` method.

```python
question = "What is AI?"
answer, passages = pipeline.run(question, retrieve_size=50, use_passage_count=4) # use 50 passages for reranking, and use top-4 passages to generate answer after reranking
print(answer)
```
