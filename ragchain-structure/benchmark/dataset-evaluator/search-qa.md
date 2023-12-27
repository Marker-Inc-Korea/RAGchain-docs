너무 커서 mrqa에서 가져왔다는거 언급하기
# Overview



StartegyQA is a open-domain question answering dataset based on Wikipedia articles. It contains questions and answers about Wikipedia articles.
Also, all questions are multi-hop question, which needs to retrieve multiple paragraphs to answer the question.
It is great for evaluating performance of your pipeline's reasoning ability.
Currently, we do not support answer evaluation for this dataset, because all answer type in this dataset is True/False.
You can easily access answer of each question using `EvaluateResult.each_results` property.

[Github](https://github.com/nyu-dl/dl4ir-searchQA)
[Paper](https://arxiv.org/abs/1704.05179)

Raw natural qa dataset is too large, so we use natural questions short qa by lucadiliello generated at mrqa 2021 in huggingface.
<br> 
[link](https://huggingface.co/datasets/lucadiliello/naturalquestionsshortqa)


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
