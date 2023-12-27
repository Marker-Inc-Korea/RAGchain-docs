너무 커서 mrqa에서 가져왔다는거 언급하기
단답충이라 잘 안될 수도 있다 언급 -> 이건 모든 단답충 데이터셋에 언급하기
# Overview

We generate question-answer pairs using data from the 'Jeopardy!' TV show. 
Each pair is associated with a specific context, which is a snippet obtained from a Google search query.
The LLM answer metric may be inaccurate because the answers in the dataset are short-answer.

[Github](https://github.com/nyu-dl/dl4ir-searchQA)
[Paper](https://arxiv.org/abs/1704.05179)



# Example Use

```Python
from RAGchain.benchmark.dataset import StrategyQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = StrategyQAEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
