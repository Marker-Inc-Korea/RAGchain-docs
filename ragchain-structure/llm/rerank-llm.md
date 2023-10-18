# Rerank LLM

### Overview

The `RerankLLM` class is made for using reranker easily, integrated to retrieval and LLM models. To use this class, you can use [`Reranker`](../reranker/) easily without extra work. For further information about reranker, please check out Reranker documentation.

In this module, first retrieval retrieves passages. Then reranker reranks retrieved passages. Finally, put retrieved passages to LLM model.&#x20;

## Usage

#### Initialize

To create an instance of `RerankLLM`, you need to provide an instance of a [`Retrieval`](../retrieval/) class and [`Reranker`](../reranker/) class. Optionally, you can specify the [name of the LLM model](./#use-custom-llm), the base URL of the LLM API endpoint, a [custom prompt](./#use-custom-prompt) function and a [streaming](./#stream-answers) function.

```python
from RAGchain.llm.rerank import RerankLLM
from RAGchain.retrieval import BM25Retrieval
from RAGchain.reranker import MonoT5Reranker

retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path") 
reranker = MonoT5Reranker()
llm = RerankLLM(retrieval=retrieval, reranker=reranker, retrieve_size=50, use_passage_count=4) # use 50 passages for reranking, and use top-4 passages to generate answer after reranking
```

#### Ask

You can ask a question to the LLM model and get an answer as well as used passages using `ask` method.

```python
question = "What is AI?"
answer, passages = llm.ask(question)
print(answer)
```

\


