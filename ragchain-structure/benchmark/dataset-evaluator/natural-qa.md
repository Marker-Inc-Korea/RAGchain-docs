너무 용량이 커서 미리 preprocessing된걸 씀
mdqa task에서 가져온걸 씀.

# Overview

The Natural Questions (NQ) dataset, introduced by Google, consists of real user queries issued to Google Search 
and answers derived from Wikipedia by annotators. Its primary purpose is to train and evaluate automatic question answering systems.

Each example in the dataset consists of a Google query and a corresponding Wikipedia page. 
The Wikipedia page has a passage or long answer annotated on it that answers the question, 
along with one or more short spans from the annotated passage containing the actual answer. 
We use long answers in this task.<br>
Further information if you want, Refer to below link!

[Github](https://github.com/google-research-datasets/natural-questions)
[Paper](https://research.google/pubs/natural-questions-a-benchmark-for-question-answering-research/)

Raw natural qa dataset is too large, so we use natural questions short qa by lucadiliello generated at mrqa 2021 in huggingface.
<br> 
link: https://huggingface.co/datasets/lucadiliello/naturalquestionsshortqa


# Example Use

```Python
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
