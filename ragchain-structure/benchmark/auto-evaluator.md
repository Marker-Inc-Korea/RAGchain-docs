# Overview

The `AutoEvaluator` class in the RAGchain framework is used for evaluating metrics without the need for ground truths. You only need to pass the questions and your pipeline for evaluation. 
It will evaluate context precision, which measures retrieval performance. And answer relevancy and faithfulness can measure answer generation performance of your pipeline.
It uses [ragas](https://github.com/explodinggradients/ragas) metrics for evaluation without ground truths.

# Example Use

```Python
from RAGchain.benchmark import AutoEvaluator

pipeline = <your pipeline>
questions: list[str] = <your list of questions>

evaluator = AutoEvaluator(pipeline, questions)
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)

# print result DataFrame
print(result.each_results)
```
