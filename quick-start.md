# Quick Start

## Installation

```
pip install RAGchain
```

For more details, see our [Installation guide.](installation.md)

## Run Simple RAG workflow

The fastest way to use RAGchain is using [pipeline](pipeline/README.md). In this example, we use [`BasicIngestPipeline`](pipeline/basicingestpipeline.md) and [`BasicRunPipeline`](pipeline/basicrunpipeline.md), which is simple but powerful.

### Setup

Before run pipelines, you need to make Redis DB. It is essential part for link retrieval and DB. Please read [`Linker`](utils/linker/README.md) docs for more information.

Great way to make Redis DB is using free Redis.com DB. Go to [redis.com](https://redis.com/try-free/) and make your database.

After you build your own Redis DB, you can get redis host url, port number, db name (number like 0), and password. You must set that values to environment variable like below.

```python
import os

os.environ["REDIS_HOST"] = "your_redis_host"  # replace with your Redis host
os.environ["REDIS_PORT"] = "your_redis_port"  # replace with your Redis port
os.environ["REDIS_DB_NAME"] = "your_redis_db_name"  # replace with your Redis database name
os.environ["REDIS_PW"] = "your_redis_password"  # replace with your Redis password (if applicable)
```

We want to use Vector DB retrieval and openai embedding in this example. So, you have to set your OpenAI API key. Set openai API key environment variable like below:

```python
os.environ["OPENAI_API_KEY"] = "your-api-key"
```

### Ingest your files

Then, you can ingest file. Prepare your .txt file. And run [`BasicIngestPipeline`](pipeline/basicingestpipeline.md) like below.&#x20;

```python
from RAGchain.pipeline.basic import BasicIngestPipeline
from RAGchain.DB import PickleDB
from langchain.document_loaders import TextLoader
from RAGchain.utils.vectorstore import ChromaSlim
from RAGchain.retrieval import VectorDBRetrieval
from RAGchain.utils.embed import EmbeddingFactory
import chromadb

chroma_db = ChromaSlim(
    client=chromadb.PersistentClient(path="your/path/to/chroma"),
    collection_name='test-collection-name',
    embedding_function=EmbeddingFactory('openai').get()
)
pipeline = BasicIngestPipeline(
    file_loader=TextLoader('your/path/to/file.txt'),
    db=PickleDB('your/path/to/db.pkl'),
    retrieval=VectorDBRetrieval(chroma_db)
)

pipeline.run()
```

In this example, we use [`PickleDB`](ragchain-structure/db/pickle-db.md) for simple saving to local disk. And use [`TextLoader`](https://api.python.langchain.com/en/latest/document\_loaders/langchain.document\_loaders.text.TextLoader.html?highlight=textloader#langchain.document\_loaders.text.TextLoader) for ingesting .txt file. And we use VectorDBRetrieval for simple dense passage retireval. As vector db, we use [`ChromaSlim`](utils/slim-vector-store/chroma-slim.md).&#x20;

You have to set path to location that you want to store chroma and pickle db.

When you run above code, [`BasicIngestPipeline`](pipeline/basicingestpipeline.md) automatically load your .txt file, split into passages, and save it to DB. Also, passage contents embeds to vector represnetation and save to Chroma vector DB.

### Run your RAG workflow

After ingestion, you can simply run RAG workflow using [`BasicRunPipeline`](pipeline/basicrunpipeline.md) like below.

```python
from RAGchain.pipeline.basic import BasicRunPipeline
from langchain.llms.openai import OpenAI

run_pipeline = BasicRunPipeline(retrieval=VectorDBRetrieval(chroma_db), llm=OpenAI())

question = "Type your own question at here"
answer = run_pipeline.run.invoke({"question": question})
print(answer)
```

While running above code, retrieval automatically retrieve related passages to your question. And, it uses OpenAI model, generate great answer to your question according to retrieved passages in your text file.&#x20;

That's it! Now you can do question\&answering about your files using LLM.

## Unlock power of RAGchain

You can use various kind of [`Retrieval`](ragchain-structure/retrieval/README.md), [`LLM`](ragchain-structure/llm/README.md), [Reranker](ragchain-structure/reranker/README.md). 
Also, you can use whole workflow easily using another [pipelines](pipeline/README.md).&#x20;

Plus, you can load various kind of files, embed contents with embedding models, store vectors at various vector stores which compatible with Langchain.&#x20;
Also, you can use Langchain LCEL with RAGchain, so using various LLM models is really easy.&#x20;

Lastly, please feel free to ask and contribute to RAGchain at [issues tab](https://github.com/NomaDamas/RAGchain/issues) in our git repo!
