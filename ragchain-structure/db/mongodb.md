# MongoDB

## Overview

The MongoDB class is designed to interact with a MongoDB database for storing and retrieving passage contents. It provides methods for creating, loading, saving, fetching, and searching passages in a MongoDB collection.

## Usage

### 1. Make MongoDB Instance with Your MongoDB

To start using the MongoDB class, you first need to create an instance of the class. You can do this by providing the URL of your MongoDB server, the name of your database, and the name of your collection.

```python
from RAGchain.DB import MongoDB

mongo_db = MongoDB(
    mongo_url="mongodb://localhost:27017",  # replace with your MongoDB server URL
    db_name="my_database",  # replace with your database name
    collection_name="my_collection"  # replace with your collection name
)
```

### 2. Use create\_or\_load

The `create_or_load` method is used to either create a new collection if it does not exist, or load an existing collection.

```python
mongo_db.create_or_load()
```

### 3. Save Passage

You can save passages to your MongoDB collection using the `save` method. This method accepts a list of Passage objects.

```python
passages = [...]  # replace with your list of Passage objects
mongo_db.save(passages)
```

### 4. Fetch Data

The `fetch` method allows you to retrieve passages from your MongoDB collection by their IDs. This method returns a list of Passage objects.

```python
ids = [...]  # replace with your list of IDs. They can be UUID or string.
fetched_passages = mongo_db.fetch(ids)

# Print the fetched passages
for passage in fetched_passages:
    print(passage)
```

### 5. Search Data

You can search for passages in your MongoDB collection using the `search` method. This method accepts filters such as passage ID, content, filepath, and metadatas, then returns a list of [Passage ](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage)objects that match the filters.

```python
search_results = mongo_db.search(content=["search term"], # replace "search term" with your search term
                                 my_metadata_key=["search metadata"]) # replace "my_metadata_key" with your metadata key
                                 # replace "search metadata" with your metadata search term

# Print the search results
for result in search_results:
    print(result)
```

Please replace the placeholders with your actual data. Also, make sure that your MongoDB server is running and accessible at the provided URL.

