# Win32HwpLoader Class

## Overview

The `Win32HwpLoader` class is a base loader for loading HWP files in a Windows environment. It uses the `pywin32` library to facilitate this process. The class can handle both `.hwp` and `.hwpx` file formats.

The primary use of this class is to extract all paragraphs and tables from a given HWP or HWPX file. It returns a list of `Document` objects, with the first `Document` containing all paragraphs excluding any text within tables. 
Each subsequent `Document` represents a table from the original file, with its content converted into HTML format. This allows you to handle complex table structures with ease.

The `Document` objects also contain metadata such as the `source` for file path and the `page_type`, which can either be 'text' or 'table'.

However, please note that `Win32HwpLoader` is only suitable for Windows. If you need to handle HWP files on macOS or Linux, consider using [`RustHwpLoader`](./rust-hwp-loader.md).

## Usage

To use the `Win32HwpLoader` class, you need to initialize it with the path to the HWP file:

```python3
loader = Win32HwpLoader('path/to/hwp/file')
```

After initializing the loader, you can call either the `load` or `lazy_load` method to extract the documents:

```python3
documents = loader.load()
```

or

```python3
for document in loader.lazy_load():
    # process document
```

The `load` method loads all documents at once into a list, while the `lazy_load` method returns a generator iterator that yields one `Document` at a time. 
This can be useful for larger files as it allows you to process each `Document` individually, reducing memory usage.

Please note that the `preprocessor` method is called internally by `load` and `lazy_load` to handle the actual extraction and conversion of the HWP file content. It's not intended to be called directly.

In case the file extension is neither `.hwp` nor `.hwpx`, a `ValueError` will be raised.
