# Ko-Strategy-QA Loader

## Overview

The `KoStrategyQALoader` is a class that loads the [KoStrategyQA](https://huggingface.co/datasets/NomaDamas/Ko-StrategyQA) dataset, which is the Korean version of the [StrategyQA](https://allenai.org/data/strategyqa) dataset. This dataset consists of multi-hop questions that require information from multiple passages to answer.

### Usage

To use this class, you would need to instantiate it and then call its load method:

```python
from RAGchain.preprocess.loader import KoStrategyQALoader

loader = KoStrategyQALoader()
documents = loader.load()
```
