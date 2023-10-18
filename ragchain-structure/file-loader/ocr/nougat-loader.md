---
description: NougatPDFLoader Class Documentation
---

# Nougat Loader

## Overview

The `NougatPDFLoader` class is a powerful tool for loading academic document PDF files. It leverages the capabilities of the Nougat model, developed by Meta, to provide an accurate conversion of academic papers from PDF format.&#x20;

## Usage

### Run Nougat API sever&#x20;

You must run Nougat API server for using this loader. You will need server with CUDA installed for running nougat model properly. More detailed installation of nougat, please go to [official github repo](https://github.com/facebookresearch/nougat).

#### Use Docker (Recommend)

First, clone facebookresearch/nougat repository to your machine, and move to docker folder.

```bash
git clone https://github.com/facebookresearch/nougat.git
cd nougat/docker
```

Then, build and run your docker container following this [instruction](https://github.com/facebookresearch/nougat/tree/main/docker).&#x20;

#### Use pip

First, install nougat package api version using pip.

```bash
pip install "nougat-ocr[api]"
```

Then, run api server with this command.

```bash
nougat_api
```

### Initialization

After runs your Nougat API server, you first need to create an instance by providing two parameters: `file_path` and `nougat_host`.

* **file\_path**: This is a string representing the path to your PDF file.
* **nougat\_host**: This is a string representing the host address where your Nougat API server is running.

Example:

<pre class="language-python"><code class="lang-python"><strong>from RAGchain.preprocess.loader import NougatPDFLoader
</strong><strong>
</strong><strong>loader = NougatPDFLoader(file_path="path/to/your/file.pdf", nougat_host="http://localhost:5000")
</strong></code></pre>

During initialization, it checks if it can establish a connection with the provided Nougat server host. If it cannot establish a connection, it raises a ValueError.

### Loading Documents

The class provides two methods for loading documents: `load()` and `lazy_load()`.

Both methods accept three optional parameters:

* **split\_section** (default True): If set to True, it splits the document by section.
* **split\_table** (default True): If set to True, it splits the document by table.
* You can also pass other arguments such as start page number (`start`) or stop page number (`stop`) as keyword arguments (`kwargs`). These are optional parameters specifying which pages of your PDF you want to load.

Example:

```python
documents = loader.load(split_section=True, split_table=False)
```

or

```python
for doc in loader.lazy_load(split_section=True):
    # process each document here...
```

These methods return instances of Document objects that contain processed content from your PDF file.
