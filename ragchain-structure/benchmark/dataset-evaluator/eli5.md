# Overview
ELI5, a dataset of long-form answers, consists of 270K threads sourced from the Reddit forum "Explain Like I'm Five" (ELI5),
where an online community provides answers to questions which are comprehensible by five year olds.
Questions and answers are from the ELI5 forum up to July 2018 and then filter it based on how users rated these pairs.
Documents, serving as web sources related to the questions, exclude Reddit, with each document representing the extracted text from a single page in the
Common Crawl dataset.

In this evaluator, we use the dataset that is collected from https://huggingface.co/datasets/Pakulski/ELI5-test.
Because of the large size of the raw dataset, we use the dataset that Pakulski has already processed.

[Github](https://github.com/facebookresearch/ELI5)<br>
[hompage](https://facebookresearch.github.io/ELI5/explore.html)<br>
[Paper](https://arxiv.org/abs/1907.09190)

# Example Use

```python
from RAGchain.benchmark.dataset import Eli5Evaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = Eli5Evaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
