# RustHwpLoader

## Overview

The `RustHwpLoader` is a Python class that loads HWP files using the [`libhwp`](https://blog.hanlee.io/2022/hwp-rs) library. It works across all OS.

This loader extracts all paragraphs and tables from the HWP file and returns them as a list of `Document` objects. Each `Document` object includes the content of the paragraph or table and some associated metadata. 
The first `Document` contains all paragraphs from the HWP file, including the texts within each table. Subsequent `Documents` represent the paragraphs within each table.

Unfortunately, this loader does not distinguish between rows and columns in a table.

The `metadata` attribute of each `Document` includes the file path (under the 'source' key) and the page type ('text' or 'table').

While other HWP loaders may offer more great features, `RustHwpLoader` is a great option for MacOS and Linux users because it does not require an external HWP loader server or a Windows-only HWP program.

## Usage

### Initialization

To use the `RustHwpLoader`, you first need to initialize it with the path to the HWP file:

```python
loader = RustHwpLoader("/path/to/hwp/file")
```

If the `libhwp` library is not installed, an `ImportError` will be raised with a message asking you to install it using pip:

```python
pip install libhwp
```

### Loading Documents

The `RustHwpLoader` provides two methods to load `Document` objects from the HWP file: `load` and `lazy_load`.

#### `load`

The `load` method returns a list of all `Documents`:

```python
documents = loader.load()
```

#### `lazy_load`

The `lazy_load` method is a generator that lazily yields `Document` objects:

```python
for document in loader.lazy_load():
    # process document
```

This method is useful when working with large HWP files that could consume a lot of memory if fully loaded into a list.

Each `Document` yielded by `load` or `lazy_load` contains a `page_content` string and a `metadata` dictionary. 
The `metadata` includes the 'source' key (the file path) and the 'page_type' key (either 'text' or 'table').
