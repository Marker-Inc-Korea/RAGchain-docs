---
description: DeepdoctectionPDFLoader Class Documentation
---

# Deepdoctection Loader

## Overview

The `DeepdoctectionPDFLoader` class is a powerful tool for loading academic document PDF files. 
It leverages the capabilities of the Deepdoctection model, developed by deepdoctection, to provide an accurate conversion of academic papers from PDF format.&#x20;

## Usage

### Run Deepdoctection API sever&#x20;

You must run Deepdoctection API server for using this loader. 
You will need server with CUDA installed for running deepdoctection model properly. More detailed installation of deepdoctection, please go to [official github repo](https://github.com/deepdoctection/deepdoctection).

#### Use Docker (Recommend)

First, clone NomaDamas/deepdoctection repository to your machine, and move to docker/NomaDamas-api-server folder.

```bash
git clone https://github.com/NomaDamas/deepdoctection-api-server.git
cd deepdoctection-api-server/docker/NomaDamas-api-server
```

Then, build and run your docker container following this [instruction](https://github.com/NomaDamas/deepdoctection-api-server/tree/master/docker/NomaDamas-api-server).&#x20;

#### Use Local Environment

First, clone NomaDamas/deepdoctection-api-server repository to your machine, and move to folder.

```bash
git clone https://github.com/NomaDamas/deepdoctection-api-server.git
cd deepdoctection-api-server
```

Then, run api server with this command.

```bash
python3 setup.py install
python3 app.py
```

### Initialization

After runs your Deepdoctection API server, you first need to create an instance by providing two parameters: `file_path` and `deepdoctection_host`.

* **file\_path**: This is a string representing the path to your PDF file.
* **deepdoctection\_host**: This is a string representing the host address where your Deepdoctection API server is running.

Example:

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.preprocess.loader import DeepdoctectionPDFLoader
</strong><strong>
</strong><strong>loader = DeepdoctectionPDFLoader(file_path="path/to/your/file.pdf", deepdoctection_host="http://localhost:8000")
</strong></code></pre>

During initialization, it checks if it can establish a connection with the provided Deepdoctection server host. If it cannot establish a connection, it raises a ValueError.

### Loading Documents

The class provides two methods for loading documents: `load()` and `lazy_load()`.



Example:

```python
documents = loader.load()
```

or

```python
for doc in loader.lazy_load():
    # process each document here...
```

These methods return instances of Document objects that contain processed content from your PDF file.
