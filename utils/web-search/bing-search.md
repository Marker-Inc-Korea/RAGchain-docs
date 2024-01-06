---
description: Bing Search Class Documentation
---

# BIng Search

## Overview
The `BingSearch` class is a part of the `RAGchain` project's `websearch` module.
It is designed to interact with the Bing Search API and retrieve search results.
The class wraps the results in a `Passage` object for further processing.

The `BingSearch` class uses the `BingSearchAPIWrapper` from the `langchain` utilities.
It returns a list of dictionaries as the search results. Each dictionary represents a search result.

## Usage
First, you need to set up the proper API keys and environment variables.
To set it up, create the `BING_SUBSCRIPTION_KEY` in the [Azure Portal](https://portal.azure.com/#home)
and a `BING_SEARCH_URL`

```Python
import os

os.environ["BING_SUBSCRIPTION_KEY"] = "<key>"
os.environ["BING_SEARCH_URL"] = "https://api.bing.microsoft.com/v7.0/search"
```

To use the BingSearch class, you need to instantiate it.

After that, you can call the `get_search_data` method to perform a search. This method requires a query string and optionally, the number of results you want to retrieve.

Here is a basic example of how to use the `BingSearch` class:
```Python
from RAGchain.utils.websearch import BingSearch

# Instantiate the BingSearch class
search = BingSearch()

# Perform a search
query = "Your search query here"
num_results = 5  # Optional, defaults to 5

passages = search.get_search_data(query, num_results)

# 'passages' now contains a list of Passage objects
```
Each `Passage` object in the `passages` list represents a search result. You can interact with these `Passage` objects as per your requirements.
