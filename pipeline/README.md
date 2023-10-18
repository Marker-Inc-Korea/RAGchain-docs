---
description: Pipeline Documentation
---

# Pipeline

## Overview

The RAGchain framework pipeline is a pre-constructed workflow in the RAGchain framework, designed to simplify and streamline the process of setting up and running a RAG system.

In other words, think of it as a cookbook: it provides you with recipes for different workflows that you can choose from. Instead of having to gather all your ingredients (components) and figure out how they work together on your own, you simply select an option from this 'cookbook', which already has all these details sorted out for you.

### Why Use Pipelines?

Building an entire workflow from scratch can be complex and time-consuming. The pipeline approach offers several advantages:

1. **Simplicity**: Pipelines abstract away many underlying complexities involved in setting up a workflow. Just call pipeline, and use it.
2. **Efficiency**: Using pipelines allows developers to leverage pre-built workflows, saving time and effort.

### Using Pipelines

To use a pipeline within the RAGchain framework:

1. Choose an appropriate pipeline based on your specific requirements.
2. Configure options as per your need.
3. Run the chosen pipeline.

Here's an example using [`BasicRunPipeline`](basicrunpipeline.md):

```python
from RAGchain.pipeline.basic import BasicRunPipeline
from RAGchain.retrieval import BM25Retrieval

pipeline = BasicRunPipeline(retrieval=BM25Retrieval(save_path="your-bm25.pkl"))
question = "What is the purpose of RAGchain project?"
answer, passages = pipeline.run(question)
```

### Building Your Own Pipeline

While we provide various pipelines for convenience, we also understand that developers may want more control over their workflows or require something unique that isn't covered by our existing pipelines.

You're free to build your own custom pipelines using individual components provided by our framework if none of our pre-built pipelines meet your specific needs.
