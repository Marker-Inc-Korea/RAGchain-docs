---
description: Google Search Class Documentation
---

# Google Search

## Overview
The `GoogleSearch` class is a part of the `RAGchain` project's `websearch` module.
It is designed to interact with the Google Search API and retrieve search results.
The class wraps the results in a `Passage` object for further processing.

The `GoogleSearch` class uses the `GoogleSearchAPIWrapper` from the `langchain` utilities.
It returns a list of dictionaries as the search results. Each dictionary represents a search result.

## Usage
First, you need to set up the proper API keys and environment variables. 
To set it up, create the `GOOGLE_API_KEY` in the [Google Cloud credential console](https://console.cloud.google.com/apis/credentials) 
and a `GOOGLE_CSE_ID` using the [Programmable Search Engine](https://programmablesearchengine.google.com/controlpanel/create).

```Python
import os

os.environ["GOOGLE_CSE_ID"] = ""
os.environ["GOOGLE_API_KEY"] = ""
```

To use the GoogleSearch class, you need to instantiate it.

After that, you can call the `get_search_data` method to perform a search. This method requires a query string and optionally, the number of results you want to retrieve. 
It also accepts search parameters as an optional dictionary.

Here is a basic example of how to use the `GoogleSearch` class:

```Python
from RAGchain.utils.websearch import GoogleSearch

# Instantiate the GoogleSearch class
search = GoogleSearch()

# Perform a search
query = "Your search query here"
num_results = 5  # Optional, defaults to 5
search_params = {}  # Optional, defaults to None

passages = search.get_search_data(query, num_results, search_params)

# 'passages' now contains a list of Passage objects
```

Each `Passage` object in the `passages` list represents a search result. You can interact with these `Passage` objects as per your requirements. 