# Overview

MSMARCO (Microsoft Machine Reading Comprehension) is a large scale dataset focused on machine reading comprehension, question answering, and passage ranking.
It contains questions, passages and answers.
The passages are top-k results Bing engin searched based on question. And when human editor created answers, they refer to these passages and selected the passages.

MSMARCO V1.1 was a original question answering dataset dataset with 100,000 real Bing questions and human-generated answers. 
Since then, several other datasets have been released, including a 1,000,000 question dataset, 
a natural language generation dataset, a passage ranking dataset, a keyphrase extraction dataset, a web crawling dataset, and an interactive search dataset.
More information about MSMARCO dataset, refer to below link! <br>
[msmarco official github](https://github.com/microsoft/MSMARCO-Question-Answering)

MSMARCOEvaluator also support rank aware metrics like NDCG, AP, CG, IDCG, RR, etc.


# Example Use
Note: 
- MSMARCO dataset version is optional(v1.1 or 2.1). Default is v1.1. 
We use validation set in v2.1 because v2.1 passage data `is_selected` values are all -1.<br>
Ingest size must be same or larger than evaluate size.

```python
from RAGchain.benchmark.dataset import MSMARCOEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = MSMARCOEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
