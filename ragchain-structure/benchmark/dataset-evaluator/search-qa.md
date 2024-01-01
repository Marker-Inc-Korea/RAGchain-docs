# Overview

The SearchQA question-answer pairs originate from J! Archive2, which comprehensively archives all question-answer pairs 
from the renowned television show Jeopardy! The passages, sourced from Google search web page snippets.
We offer passage metadata, encompassing details like 'air_date,' 'category,' 'value,' 'round,' and 'show_number,'
enabling you to enhance retrieval performance at your discretion.
Should you require further details about SearchQA, please refer to below links.

[Github](https://github.com/nyu-dl/dl4ir-searchQA)<br>
[Paper](https://arxiv.org/abs/1704.05179)

# Example Use
Note:
- The LLM answer metric may be inaccurate because the answers in the dataset are short-answer.

```python
from RAGchain.benchmark.dataset import SearchQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = SearchQAEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
