# Overview

DSTC11-Track5 is a dataset from the DSTC11-Track5 competition. 
This dataset is a task-oriented dialogue dataset, and the task is to build a dialogue system that assists users 
in accomplishing specific goals, such as booking a hotel or a restaurant.

In this evaluator, we generated questions as prompts from the dialogue context between the user and the system.
Passages are generated from the review posts selected 33 hotels and 110 restaurants from MultiWOZ, and collect 10 reviews for each entity. 
On  average, each review contains 5.6 sentences and 56.71 tokens. 
The answers are responses from the system.
Further information about DSTC11-Track5, please refer to below links.

[HuggingFace](https://huggingface.co/datasets/NomaDamas/DSTC-11-Track-5)<br>
[Github](https://github.com/alexa/dstc11-track5)<br>
[hompage](https://dstc11.dstc.community/)<br>
[Paper](https://arxiv.org/abs/2305.12091)

# Example Use

```python
from RAGchain.benchmark.dataset import DSTC11Track5Evaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = DSTC11Track5Evaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
