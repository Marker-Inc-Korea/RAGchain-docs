# Overview

The Natural Questions (NQ) dataset, introduced by Google, consists of real user queries issued to Google Search 
and answers derived from Wikipedia by annotators. Its primary purpose is to train and evaluate automatic question answering systems.

Each example in the dataset consists of a Google query and a corresponding Wikipedia page. 
The Wikipedia page has a passage or long answer annotated on it that answers the question, 
along with one or more short spans from the annotated passage containing the actual answer.<br>

<br>
Further information if you want, Refer to below link!<br>

[Github](https://github.com/google-research-datasets/natural-questions)<br>
[Paper](https://research.google/pubs/natural-questions-a-benchmark-for-question-answering-research/)

Raw natural qa dataset is too large,
This split is derived from the MRQA 2019 Shared Task, and has been formatted and filtered specifically 
for Question Answering. If you want to refer to the original dataset, please refer to this
[link](https://huggingface.co/datasets/lucadiliello/naturalquestionsshortqa).


# Example Use
Note:
- The dataset answers are short spans, so answer evaluation scores might be inaccurate.<br>

```python
from RAGchain.benchmark.dataset import NaturalQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = NaturalQAEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
