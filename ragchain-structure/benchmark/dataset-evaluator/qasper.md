# Overview

Qasper is question answering dataset based on NLP papers. It contains full text (plus figures and tables captions) in NLP paper, questions and answers about corresponding paper.
You can evaluate performance of your RAG workflow in closed-domain QA task. 

# Example Use
Note : We recommend set proper evaluate_size. This evaluator ingest each NLP paper when evaluated. 
So, if you set evaluate_size to 100, it will ingest 100 NLP papers when evaluated. It will take long time.
You can set random_state for evaluating constant questions. If you change random_state, other questions will be evaluated, even with same evaluate_size.

```Python
from RAGchain.benchmark.dataset import QasperEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = QasperEvaluator(pipeline, evaluate_size=20, random_state=60)
evaluator.ingest(retrievals, db)
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
