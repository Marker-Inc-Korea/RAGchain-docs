# Overview

TriviaQA is a question-answer-evidence triples dataset. Questions-answer pairs are collected
from 14 trivia and quiz-league websites and evidence are collected from top-k Wikipedia articles and Web search results.
We use unfiltered version of TriviaQA. Because it is not all documents for a given question contain the answer strings
contrasted RC(Reading Comprehension) version. So unfiltered dataset more appropriate for our RAG task.

[HuggingFace](https://huggingface.co/datasets/trivia_qa)<br>
[Github](https://github.com/mandarjoshi90/triviaqa)<br>
[Paper](https://arxiv.org/abs/1705.03551)

# Example Use
Notice: 
- Recommend make ingest size small in docs.
This is because when ingesting data, having one query per ground truth becomes burdensome,
especially when there are a large number of ground truths to ingest.

- The reason context_recall does not accommodate this benchmark is due to the excessive number
of retrieval ground truths that exceed the context length in ragas metrics.

```Python
from RAGchain.benchmark.dataset import TriviaQAEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = TriviaQAEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
