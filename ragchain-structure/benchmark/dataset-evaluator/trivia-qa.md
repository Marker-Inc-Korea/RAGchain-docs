# Overview

TriviaQA is a question-answer-evidence triples dataset. Questions-answer pairs are collected
from 14 trivia and quiz-league websites and evidence are collected from top-k Wikipedia articles and Web search results.
We opt for the unfiltered version of TriviaQA. This choice is made because not all documents associated with a particular
question contain the answer strings. Consequently, the unfiltered version dataset is more suitable 
for our RAG (Retrieval-Augmented Generation) task compared to the RC (Reading Comprehension) version.<br>
The LLM answer metric may be inaccurate because the answers in the dataset are short-answer.

[HuggingFace](https://huggingface.co/datasets/trivia_qa)<br>
[Github](https://github.com/mandarjoshi90/triviaqa)<br>
[Paper](https://arxiv.org/abs/1705.03551)

# Example Use
Note: 
- Recommend make ingest size small in docs.
This is because when ingesting data, having one query per ground truth becomes burdensome,
especially when there are a large number of ground truths to ingest.

- The reason context_recall does not accommodate this benchmark is due to the excessive number
of retrieval ground truths that exceed the context length in ragas metrics.

- This dataset answer is short answer. So, answer metric may be inaccurate.

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
