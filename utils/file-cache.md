# File Cache

The purpose of `FileCache` is to remove duplicate documents since users are likely to load duplicate document files if they ingest files multiple times.

The `FileCache` is a util that checks the DB for duplicate file check files.

## Usage

At first, import FileCache.

```python
from RAGchain.utils.file_cache import FileCache
from RAGchain.DB import PickleDB
from langchain.schema import Document
```

We will intentionally generate db saved duplicate files to illustrate.

```python
test_passages: List[Passage] = [
    Passage(content="test1", filepath="test1"),
    Passage(content="test2", filepath="test2"),
    Passage(content="test3", filepath="test2")
]

test_documents: List[Document] = [
    Document(page_content="ttt1211", metadata={"source": "test1"}),
    Document(page_content="asdf", metadata={"source": "test2"}),
    Document(page_content="hgh", metadata={"source": "test3"}),
    Document(page_content="egrgfg", metadata={"source": "test4"}),
    Document(page_content="hhhh", metadata={"source": "test4"}),
]
```

Create an instance and input parameter. At this example, we use [`PickleDB`](../ragchain-structure/db/pickle-db.md).

<pre class="language-python"><code class="lang-python">db = PickleDB(save_path = "your-pickle-path.pkl"))
<strong>db.creat_or_load()
</strong><strong>db.save(test_passages)
</strong><strong>file_cache = FileCache(db)
</strong></code></pre>

And then, use `delete_duplicate()` to detect what file is already saved in DB. You can get List\[Document] with duplicate document removed!

```python
test_documents = file_cache.delete_duplicate(test_documents)
```

