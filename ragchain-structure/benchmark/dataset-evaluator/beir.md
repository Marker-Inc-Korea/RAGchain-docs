# Overview

BEIR is a heterogeneous benchmark that has been built from 18 diverse datasets representing 9 information retrieval tasks.
In this project, six datasets are utilized: FEVER, FIQA, HOTPOTQA, QUORA, SCIDOCS, and SCIFACT.
More information about beir dataset, please visit link!


[Github](https://github.com/beir-cellar/beir?tab=readme-ov-file)<br>
[Paper](https://openreview.net/forum?id=wCu6T5xFjeJ)<br>
[HuggningFace](https://huggingface.co/BeIR)

The structure of our BEIR benchmark is depicted in the image below. All six benchmark datasets share 
the same basic preprocessing process. Therefore, we have encapsulated the preprocessing, ingestion, and 
evaluation processes into the BaseBeirEvaluator class. Each evaluator class, which corresponds to the benchmark datasets 
(FEVER, FIQA, HOTPOTQA, QUORA, SCIDOCS, and SCIFACT), inherits from the BaseBeirEvaluator.

![beir-structure.png](../../../.gitbook/assets/beir-structure.png)

Also, we removed non-relevant score passages at qrels.<br>

# Example Use

```python
from RAGchain.benchmark.dataset import <your beir evaluator>

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = <your beir evaluator>(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```