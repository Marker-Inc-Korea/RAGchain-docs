# Web Search

## Overview
The `WebSearch` module is a part of the `RAGchain` project's `utils` package.
It is designed to interact with various web search APIs and retrieve search results. The module contains several classes, each of which wraps a specific search API.
The results are wrapped in a `Passage` object for further processing. 

The `WebSearch` module uses the `BaseWebSearch` abstract base class to define a common interface for all search classes.
Each search class must implement the `get_search_data` method, which performs a search and returns a list of `Passage` objects.


## Supporting Search Engines

Currently, the `WebSearch` module supports the following search engines: 

- [Google Search](google-search.md)
- [Bing Search](bing-search.md)

Each search class can be used independently, and they all follow the same usage pattern. 

Instantiate the class, then call the `get_search_data` method with a query string and optionally, the number of results you want to retrieve. 
The method returns a list of `Passage` objects, each representing a search result.
