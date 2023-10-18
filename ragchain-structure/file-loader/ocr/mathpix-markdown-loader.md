# Mathpix Markdown Loader

## Overview

The `MathpixMarkdownLoader` class is a Python class that loads and processes Mathpix Markdown files (.mmd files), which are a special kind of markdown file designed for scientific papers. For the detailed explaination about mathpix markdown, please check out [mathpix website](https://mathpix.com/docs/mathpix-markdown/overview).

The class provides functionality to split the loaded file into sections and tables, making it easier to process and analyze the scientific content.

## Usage

### Initialization

To initialize the `MathpixMarkdownLoader` class, you need to provide a path to an existing Mathpix Markdown file (`.mmd`).

```python
from RAGchain.preprocess.loader import MathpixMarkdownLoader

loader = MathpixMarkdownLoader(filepath="/path/to/your/file.mmd")
```

If the provided filepath does not point to an existing file, a `ValueError` will be raised.

#### Loading Data

There are two ways you can load data from the `.mmd` file: `load()` or `lazy_load()`

Example:

```python
documents = loader.load(split_section=True, split_table=True)
```

or

```python
for document in loader.lazy_load(split_section=True, split_table=True):
    # process each Document here...
    pass
```

Both methods return list of Document objects representing each section or table in the original `.mmd` file.

#### Splitting Sections and Tables

The loader provides options for splitting content into sections and tables:

* `split_section`: Splits provided markdown content into separate sections based on '#' headers.
* `split_table`: Splits provided markdown content into separate pieces based on LaTeX table environments (`\\begin{table}` ... `\\end{table}`). The returned list alternates between non-table text and table text.

These features can be used independently of loading if desired:

```python
content = "your-markdown-string"
sections = MathpixMarkdownLoader.split_section(content)
tables_and_text = MathpixMarkdownLoader.split_table(content)
```

Note: The order of each section/table in returned list(s) is consistent with their order in original `.mmd` file.
