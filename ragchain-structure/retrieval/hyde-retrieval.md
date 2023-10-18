---
description: HyDERetrieval Class Documentation
---

# Hyde Retrieval

### Overview

The `HyDERetrieval` class is inspired by the paper "[Precise Zero-shot Dense Retrieval without Relevance Labels](https://arxiv.org/abs/2212.10496)". It uses a language model to generate a hypothetical passage for a given query and then retrieves passages using this hypothetical passage as the query.

### Usage

#### Initialize

First, prepare the retrieval instance you want to use and set up your system prompt. In this example, we are using `BM25Retrieval` as the base retrieval method and setting up a custom system prompt.

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.retrieval import BM25Retrieval, HyDERetrieval
</strong><strong>
</strong><strong>test_prompt = "Please write a scientific paper passage to answer the question"
</strong>bm25_retrieval = BM25Retrieval(save_path="path/to/your/bm25/save_path")
hyde_retrieval = HyDERetrieval(bm25_retrieval, system_prompt=test_prompt)
</code></pre>

#### Ingest

Ingest a list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage)s into the retrieval in the HyDE retrieval.

```python
passages = [ ... ] # your list of Passage objects
hyde_retrieval.ingest(passages)
```

#### Retrieve

Retrieve top-k passages for a given query. You can also specify model kwargs such as max tokens for hypothetical passage generation model.   modle kwargs reference is in [openai api docs](https://platform.openai.com/docs/api-reference/chat/object).&#x20;

```python
query = "What is visconde structure?"
top_k = 5
top_k_passages = hyde_retrieval.retrieve(query, top_k=top_k, model_kwargs={'max_tokens': 64})
```

#### Retrieve with filter

You can also filter the retrieved passages. Use the `retrieve_with_filter` method and provide the query, top-k value, and a list of content, filepath, or metadata values to filter by.&#x20;

In this method uses `DB.search` method. Please refer [here](https://nomadamas.github.io/RAGchain/build/html/RAGchain.DB.html#RAGchain.DB.base.BaseDB.search) for further information.

Here's an example:

```python
filtered_passages = hyde_retrieval.retrieve_with_filter(query, top_k, filepath=["filepath1", "filepath3"])
# This code will search top-5 most similar passages with filepath1 and filepath3
```

\
