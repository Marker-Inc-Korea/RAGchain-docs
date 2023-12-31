# Overview

Mr.TyDi is a multi-lingual benchmark dataset built on TyDi.
Mr.TyDi apply for languages that is 11 diverse languages and 1 combined diverse languages.
The passages are from Wikipedia articles in order to google search. 
Annotators classify top Wikipedia articles by relevancy and extract positive passage that is retrieval ground truth.
Mr.TyDi questions and passages are all same languages in each language datasets.
So if you want combined language datasets, you can input 'combined' at language parameter
If you want more information about Mr.TyDI, Please visit below link!
<br>[mr.tydi official github](https://github.com/castorini/mr.tydi)

The significance of this dataset is great to benchmark dataset that consist of diverse languages.
You can choose languages like below.<br>
(arabic, bengali, combined, english, finnish, indonesian, japanese, korean, russian, swahili, telugu, thai) <br>
If you want to use languages combined, You can choose 'combined' configuration.

# Example Use
Note: 
- Mr.TyDi questions and passages are all same languages in each language datasets.
If you want to combined language datasets, you can input 'combined' at language parameter.<br>
Each language datasets are not translated. They are independent question - passage datasets.

```Python
from RAGchain.benchmark.dataset import MrTydiEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = MrTydiEvaluator(pipeline, language = 'English', evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```
