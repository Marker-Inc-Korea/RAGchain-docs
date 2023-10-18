---
description: Redis DB Singleton Class Documentation
---

# Linker

## Overview

The `RedisDBSingleton` is a singleton class that manages a Redis database. It is used to link the database and passage IDs that are stored in retrievals.&#x20;

The **passage ID** is stored as the **key** in the Redis database, and the **`db_path`** of the database where the passage is stored is saved as the **value**.&#x20;

This setup allows for efficient retrieval of passages: \
given a passage ID obtained through retrieval, the `db_path` can be quickly fetched from the Redis database, and then used to retrieve the actual passage content from the correct database.&#x20;

Being a singleton, the `RedisDBSingleton` ensures that only one instance of the Redis database connection is created throughout the application, optimizing resource usage.

### Redis DB

Redis database provides high performance and in-memory data storage, making it an excellent choice for this use case. Its key-value data model allows for quick and efficient retrieval of data, optimizing the retrieval process.

## Usage

To use the [`RedisDBSingleton`](#user-content-fn-1)[^1] class, you need to provide the following environment variables:

```python
os.environ["REDIS_HOST"] = "your_redis_host"  # replace with your Redis host
os.environ["REDIS_PORT"] = "your_redis_port"  # replace with your Redis port
os.environ["REDIS_DB_NAME"] = "your_redis_db_name"  # replace with your Redis database name
os.environ["REDIS_PW"] = "your_redis_password"  # replace with your Redis password (if applicable)
```

Then, you can use RedisDB Linker to everywhere. Linker is essential for running [`Retrieval`](../ragchain-structure/retrieval/) class. So you have to set redis environment variable before using [`Retrieval`](../ragchain-structure/retrieval/).

[^1]: 
