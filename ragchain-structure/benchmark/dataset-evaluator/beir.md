# Overview

BEIR is a heterogeneous benchmark that has been built from 18 diverse datasets representing 9 information retrieval tasks.
Using project, we use 6 datasets, FEVER, FIQA, HOTPOTQA, QUORA, SCIDOCS, and SCIFACT.
More information about beir dataset, please visit link!

[Github](https://github.com/beir-cellar/beir?tab=readme-ov-file)<br>
[Paper](https://openreview.net/forum?id=wCu6T5xFjeJ)<br>
[HuggningFace](https://huggingface.co/BeIR)


Our BEIR benchmark structure is like below picture.
Basic preprocessing process is same at 6 benchmark dataset,
So we construct preprocess process, ingest, evaluation code are in BaseBeirEvaluator class.
Each evaluator class corresponding to the benchmark datasets
(FEVER, FIQA, HOTPOTQA, QUORA, SCIDOCS, and SCIFACT) inherits from the BaseBeirEvaluator.

![beir-structure.png](../../../.gitbook/assets/beir-structure.png)

Also, we removed non-relevant score passages at qrels.<br>
The significance of this dataset is diverse tasks, diverse domains, task difficulties, and diverse annotation strategies
in each dataset.

Beir test code is little different from other benchmark.
```Python
bm25_path, pickle_path = generate_path('fever')
retrieval, db, llm, pipeline = set_beir_evaluator(bm25_path, pickle_path)
evaluator = <Beir evaluator>(run_pipeline=pipeline, evaluate_size=5)
evaluator.ingest(retrievals=[retrieval], db=db, ingest_size=20)

yield evaluator
remove_path(bm25_path, pickle_path)
```
As you can see, `generate_path` function generate bm25 path and pikle path
matched dataset name. And, `set_beir_evaluator` function generate
`retrieval`, `db`, `llm`, `pipeline`. If you want to modify them, you can
set others in `set_beir_evaluator`.

# Example Use
NOTICE:
We except context_recall metric that is ragas metric.
It takes a long time in evaluation because beir token is too big.
So if you want to use context_recall metric, You can add self.retrieval_gt_ragas_metrics.

Additionally, you can preprocess datasets in this class constructor to benchmark your own pipeline.
You can modify utils methods by overriding it for your dataset.

```Python
from RAGchain.benchmark.dataset import <your beir evaluator>

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = <your beir evaluator>(pipeline, evaluate_size=5)
evaluator.ingest(retrievals=[retrieval], db=db, ingest_size=20) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```