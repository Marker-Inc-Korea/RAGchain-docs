---
description: Documentation for HwpLoader class
---

# Hwp Loader

## Overview

The `HwpLoader` class is a dedicated loader for handling HWP files, which are widely used in South Korea. It provides functionality to load and convert HWP files into text using an external API, namely the [hwp-converter-api](https://github.com/NomaDamas/hwp-converter-api).

The hwp-converter-api is a service that converts HWP files into plain text. You can find more information about this API at [here](https://github.com/NomaDamas/hwp-converter-api).

## Usage

To use this class, you would need to instantiate it by providing necessary parameters and then call its load or lazy\_load method:

```python
from RAGchain.preprocess.loader import HwpLoader

loader = HwpLoader(path="path_to_your_file.hwp", 
                   hwp_host_url="http://your_hwp_converter_api_url")
documents = loader.load()
```

You can get list of [`Document`](https://docs.langchain.com/docs/components/schema/document) objects that came from original hwp file.

Please note that currently only .hwp files are supported; .hwpx files are not supported yet by this loader.

Also note that you must have aiohttp library installed in your environment.

Lastly, ensure that provided URL points to running instance of hwa-converter-api.
