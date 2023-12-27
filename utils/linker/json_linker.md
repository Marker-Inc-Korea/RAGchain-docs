---
description: Redis Linker Class Documentation
---

# JSON Linker

## Overview
`JsonLinker` is a singleton class that allows the role of a linker
to be played locally to use JSON file without using an external DB like redisDB or dynamoDB.

The class manages JSON files. 
It is used to link database and passage IDs that are stored in retrievals. 
The class is part of the `RAGchain` project and is located in the `RAGchain/utils/linker/json_linker.py` file.  

The class inherits from the BaseLinker class and implements the put_json, get_json, and flush_db abstract methods. 


The class uses the `json` Python library to interact with a JSON file. 
It requires the `JSON_LINKER_PATH` environment variable to be set, which specifies the path to the JSON file. 

## Usage
To use the `JsonLinker` class, you first need to set the required environment variable `LINKER_TYPE`and `JSON_LINKER_PATH`.

```Python
LINKER_TYPE="json"
JSON_LINKER_PATH="json file path(name)"
```

Here is an example of how to use the `JsonLinker` class:
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
