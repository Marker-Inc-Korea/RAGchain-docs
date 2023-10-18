---
description: EmbeddingFactory Class Documentation
---

# Embedding

## Overview

The `EmbeddingFactory` class returns an Langchian's [`Embeddings`](https://python.langchain.com/docs/integrations/text\_embedding/) class according to the specified embedding type. This class simplifies the process of creating an embedding instance. It provides common embeddings used by RAG workflows.

## Usage

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.utils.embed import EmbeddingFactory
</strong><strong>
</strong><strong>openai_embedding = EmbeddingFactory(embed_type='openai', device_type='cuda').get()
</strong></code></pre>

### Supporting Embedding Models

You can use and [`Embeddings`](https://python.langchain.com/docs/integrations/text\_embedding/) in Langchain. You don't have to use `EmbeddingFactory`. But, with `EmbeddingFactory` you can easily get below embedding models.

| Model Name                                                                          | embed\_type             |
| ----------------------------------------------------------------------------------- | ----------------------- |
| [OpenAI text-embedding-ada-002](https://platform.openai.com/docs/guides/embeddings) | openai                  |
| [Contriever](https://huggingface.co/facebook/mcontriever-msmarco)                   | contriever              |
| [Multilingual-e5](https://huggingface.co/intfloat/multilingual-e5-large)            | multilingual\_e5        |
| [Ko-sroberta-multitask](https://huggingface.co/jhgan/ko-sroberta-multitask)         | ko\_sroberta\_multitask |
| [KoSimCSE](https://huggingface.co/BM-K/KoSimCSE-roberta-multitask)                  | kosimcse                |

You can put `embed_type` string of model that you want to use when initialize `EmbeddingFactory`.&#x20;
