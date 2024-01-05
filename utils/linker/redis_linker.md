---
description: Redis Linker Class Documentation
---

# Redis Linker

## Overview

The `RedisLinker` class is a singleton class that manages Redis. 
It is used to link database and passage IDs that are stored in retrievals. 
The class is part of the RAGchain project and is located in the `RAGchain/utils/linker/redis_linker.py` file.  

The class inherits from the BaseLinker class and implements the `put_json`, `get_json`, and `flush_db` abstract methods. 
It also includes additional methods such as `connection_check` and `__del__`.  

The 'RedisLinker' class uses the redis Python library to interact with a Redis database. 
It requires several environment variables to be set, including `REDIS_HOST`, `REDIS_PORT`, `REDIS_DB_NAME`, and `REDIS_PW`.
### Redis DB?

Redis database provides high performance and in-memory data storage, making it an excellent choice for this use case. Its key-value data model allows for quick and efficient retrieval of data, optimizing the retrieval process.

## Usage

To use the RedisLinker class, you first need to set the required **environment variables**. 
These include `LINKER_TYPE`, `REDIS_HOST`, `REDIS_PORT`, `REDIS_DB_NAME`, and `REDIS_PW`.
```Python
LINKER_TYPE="redisdb"
REDIS_HOST="your redis host url"
REDIS_PORT="your redis port number"
REDIS_DB_NAME="your redis db name"
REDIS_PW="your redis password"
```
Here is an example of how to use the `RedisLinker` class:
```Python
from RAGchain.utils.linker.redis_linker import RedisLinker

# Create an instance of the RedisLinker class
linker = RedisLinker()

# Check the connection to the Redis database
if linker.connection_check():
    print("Connected to Redis database")

# Put JSON data into the Redis database
linker.put_json("1234", {"name": "John", "age": 30})

# Get JSON data from the Redis database
data = linker.get_json(["1234"])
print(data)

# Flush the Redis database
linker.flush_db()
```

Please note that the `put_json` method requires a unique ID and a JSON data as parameters. 
The `get_json` method requires a list of IDs as a parameter. The `flush_db` method does not require any parameters.
