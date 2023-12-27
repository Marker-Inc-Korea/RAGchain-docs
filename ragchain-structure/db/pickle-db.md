# Pickle DB

## Overview

The PickleDB class is designed to interact with a local disk storage using pickle file format for storing and retrieving passage contents. It provides methods for creating, loading, saving, fetching, and searching passages in a pickle file.

## Usage

### 1. Make PickleDB Instance

To start using the PickleDB class, you first need to create an instance of the class. You can do this by providing the path to your pickle file.

```python
from RAGchain.DB import PickleDB

pickle_db = PickleDB(
    save_path="path/to/your/pickle/file.pkl"  # replace with your pickle file path
)
```

### 2. Use create\_or\_load

The `create_or_load` method is used to either create a new pickle file if it does not exist, or load an existing pickle file.

```python
pickle_db.create_or_load()
```

### 3. Save Passage

You can save passages to your pickle database using the `save` method. This method accepts a list of [Passage](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. The passages are saved to the pickle file and also to the [Linker](../../utils/linker/redis_linker.md).

```python
passages = [...]  # replace with your list of Passage objects
pickle_db.save(passages)
```

### 4. Fetch Data

The `fetch` method allows you to retrieve passages from your pickle database by their IDs. This method returns a list of [Passage](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects.

```python
ids = [...]  # replace with your list of IDs. They can be UUID or str.
fetched_passages = pickle_db.fetch(ids)

# Print the fetched passages
for passage in fetched_passages:
    print(passage)
```

### 5. Search Data

You can search for passages in your pickle database using the `search` method. This method accepts filters such as passage ID, content, filepath, and metadatas, then returns a list of [Passage](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects that match the filters.

```python
search_results = pickle_db.search(content=["search term"])  # replace "search term" with your search term

# Print the search results
for result in search_results:
    print(result)
```

Please replace the placeholders with your actual data. Also, make sure that your pickle file is accessible at the provided path.
