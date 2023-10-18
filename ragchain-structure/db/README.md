---
description: Store passages at traditional database
---

# DB

## Overview

Our framework currently supports two types of databases: MongoDB and PickleDB. We are planning to add more database types in the future to provide more flexibility and options for users.

#### 1. MongoDB

MongoDB is a popular NoSQL database that provides high performance, high availability, and easy scalability. It works on the concept of collections and documents, making it a good choice for storing complex and hierarchical data structures. In our framework, MongoDB is used for storing and retrieving passage contents.\
[https://www.mongodb.com](https://www.mongodb.com/)

#### 2. PickleDB

PickleDB is a super simple store. It is built upon Python's pickle module for serializing and deserializing Python object structures. PickleDB stores data in a local disk file in a pickle format, making it a good choice for small projects or for testing RAGchain quickly. We do not recommend PickleDB for production level, but it's great way to start RAGchain framework! \


### Role of the DB in the Framework

The role of the database in our framework is to store and manage passage contents and various metadatas. The database can save passages, fetch passages by their IDs, and searching for passages based on filters.

### Advantages of DBs

One of the main advantages of using databases in our framework is that you can **continue to use your existing databases**. This means you don't have to migrate your data to a new database system to use our framework.

Another advantage is that you can **use multiple databases** at the same time. This can be useful when you have data stored in different databases and you want to access all of them from our framework. Like in MongoDB, you can use lots of collections. Without using RAGchain, managing all of collections for RAG is painful. But at RAGchain, that pain will go away.&#x20;

Furthermore, using databases **frees you from limits** like the character limit for vectorDB. This means you can store and manage large amounts of data without worrying about hitting any limits.

Also, our framework allows you to perform **searches directly in the database**. This can be useful when you want to find specific passages based on various filters such as passage ID, content, filepath, and additional metadata. The search function returns a list of Passage objects that match the filters. In this way, you can easily search passages from multiple vector stores and retrievers.
