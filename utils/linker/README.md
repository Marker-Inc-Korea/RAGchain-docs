# Linker

## Overview
`linker/base.py` is a part of the RAGChain application that manages the storage of JSON data in a database. It is designed as a Singleton, a design pattern that restricts the instantiation of a class to a single instance. This is to ensure that only one instance of the Linker can be created, which is critical for maintaining data consistency and integrity in the application.

The `BaseLinker` class provides the abstract methods `put_json`, `get_json`, and `flush_db`, which must be implemented by any database-specific Linker classes. This design allows the application to easily switch between different types of databases by simply changing the Linker class.

## Importance of Linker

The Linker plays a vital role in managing the storage of JSON data in the RAGChain application. It provides a consistent interface for storing and retrieving data, regardless of the underlying database technology. This means that the rest of the application does not need to be concerned with the specifics of the database implementation.

The Singleton design of the Linker ensures that only one instance of the Linker is ever created, preventing potential data inconsistencies and ensuring that all parts of the application are working with the same data.
## Supporting Linker DB
1. [Redis Linker](redis_linker.md):
2. [Dynamo Linker](dynamo_linker.md):
3. [Json Linker](json_linker.md): 

## Usage
To use the Linker in your application, you will need to set the `LINKER_TYPE` environment variable in your `.env` file. 
This should be set to the type of database you wish to use, which must be one of `redisdb`, `dynamodb`, or `json`.

Once the `LINKER_TYPE` is set, you can create an instance of the Linker in RAGchain `__init__.py` file. 
By default, only one instance of the Linker can be created. If you attempt to create another instance, a `SingletonCreationError` will be raised.

If you need to create multiple instances of the Linker for testing purposes, you can do so by setting `allow_multiple_instances=True` when creating the Linker. 
However, we strongly recommend that you **only create one instance** for normal application use to avoid potential data inconsistencies.

Here is an example of how to create an instance of the Linker:
```Python
LINKER_TYPE="redisdb or dynamodb or json"
```