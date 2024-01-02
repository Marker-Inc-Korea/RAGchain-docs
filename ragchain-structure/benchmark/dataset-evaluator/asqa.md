# Overview

ASQA (Factoid Questions Meet Long-Form Answers) is the long-form question answering dataset 
based on ambiguous factoid questions. ASQA task are not derived from information retrieval task, but answer evaluation task.
It is not suitable for evaluating retrieval performance. So we provide answer evaluation metric and ingest
crawled wikipedia documents to db for evaluating answer performance.


[HuggingFace](https://huggingface.co/datasets/din0s/asqa)<br>
[Github](https://github.com/google-research/language/tree/master/language/asqa)<br>
[Paper](https://arxiv.org/abs/2204.06092)

# Example Use
Note:
- Recommend make ingest size small in docs.
  This is because when ingesting data, having one query per ground truth becomes burdensome,
  especially when there are a large number of ground truths to ingest.

```Python
from RAGchain.benchmark.dataset import ASQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = ASQAEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
