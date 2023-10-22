# Overview

Ko-Strategy-QA is Korean version of Strategy-QA, which is translated by DeepL.
Ko-Strategy-QA is the only option for evaluating multi-hop questions in Korean.
Also, RAGchain makers made this dataset^^

# Example Use
    
```Python
from RAGchain.benchmark.dataset import KoStrategyQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = KoStrategyQAEvaluator(pipeline, evaluate_size=100)
evaluator.ingest(retrievals, db) # This code will ingest whole paragraphs in Ko-Strategy-QA dataset. You only need to run this once.
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
