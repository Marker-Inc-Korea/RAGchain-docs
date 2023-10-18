---
description: EvidenceExtractor Class Documentation
---

# Evidence Extractor

## Overview

The `EvidenceExtractor` class is a utility that extracts relevant evidences from a list of passages based on a given question. It uses a Language Model (LLM) to identify and return the relevant fragments from the original passages.

## Usage

### Initialize

To use the `EvidenceExtractor` class, you first need to create an instance of the class.&#x20;

```python
from RAGchain.utils.evidence_extractor import EvidenceExtractor

extractor = EvidenceExtractor()
```

You can put additional parameter `model_name` and `api_base` for using custom model. Plus, you can put custom system prompt for extracting evidence. If not, default english prompt will be used.

### Extract

After the `EvidenceExtractor` instance has been initialized, you can use the `extract` method to extract relevant evidences from a list of passages based on a given question. The `extract` method takes a question (a string) and a list of passages as input and returns the extracted relevant evidences.

```python
question = "What is the atomic number of hydrogen?"
passages = [
    Passage(content="Hydrogen is the first atom in atomic table."),
    Passage(content="Is is lighter than air so it floats."),
    Passage(content="Hydrogen can cause fire.")
]
result = extractor.extract(question, passages)
```

The `extract` method returns a string containing the extracted relevant evidences. If there is no evidence related to the question in the passages, it returns 'No Fragment' if you are using default prompt.
