---
description: Dynamo Linker Class Documentation
---

# Dynamo Linker

## Overview

The `DynamoLinker` class is a singleton class that manages DynamoDB. 
It is used to link database and passage IDs that are stored in retrievals.
The class is part of the `RAGchain` project and is located in the `RAGchain/utils/linker/dynamo_linker.py` file.  

The class inherits from the `BaseLinker` class and implements the `put_json`, `get_json`, and `flush_db` abstract methods. 
 
The DynamoLinker class uses the `boto3` Python library to interact with a DynamoDB database. 
It requires several environment variables to be set, including `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`, and `DYNAMODB_TABLE_NAME`.

### Dynamo DB?
Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. 
DynamoDB lets you offload the administrative burdens of operating and scaling a distributed database so that you don't have to worry about hardware provisioning, 
setup and configuration, replication, software patching, or cluster scaling. 
DynamoDB also offers encryption at rest, which eliminates the operational burden and complexity involved in protecting sensitive data. 

## Usage
To use the DynamoLinker class, you first need to set the required **environment variables**.
These include `LINKER_TYPE`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`, and `DYNAMODB_TABLE_NAME`.

```Python
LINKER_TYPE="redisdb"
AWS_ACCESS_KEY_ID="your aws access key id"
AWS_SECRET_ACCESS_KEY="your aws secret access key"
AWS_REGION="your AWS region"
DYNAMODB_TABLE_NAME="your dynamoDB table name"
```
The DynamoLinker class will automatically create a DynamoDB table if it does not exist. 
If a table with the specified name already exists, the class will import and use the existing table.

Here is an example of how to use the `DynamoLinker` class:
```Python
from RAGchain.utils.linker.dynamo_linker import DynamoLinker

# Create an instance of the DynamoLinker class
linker = DynamoLinker()

# Check the connection to the DynamoDB database
if linker.connection_check():
    print("Connected to DynamoDB database")

# Put JSON data into the DynamoDB database
linker.put_json("1234", {"name": "John", "age": 30})

# Get JSON data from the DynamoDB database
data = linker.get_json(["1234"])
print(data)

# Flush the DynamoDB database
linker.flush_db()
```
Please note that the `put_json` method requires a unique ID and a JSON data as parameters. 
The `get_json` method requires a list of IDs as a parameter. 
The `flush_db` method does not require any parameters.