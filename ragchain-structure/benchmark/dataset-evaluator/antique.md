# Overview

ANTIQUE comprises 2,626 open-domain non-factoid questions sourced from various categories, with a total of 34,011 
manually annotated relevance judgments. These questions originated from real users on Yahoo! Answers, a community 
question answering service. The process of gathering relevance judgments for all corresponding answers involved crowdsourcing.

It is great to evaluate retrieval performance because this dataset designed for information retrieval benchmark.

[antique ir_datasets](https://ir-datasets.com/antique.html)<br>
[Homepage](https://ciir.cs.umass.edu/downloads/Antique/)<br>
[Paper](https://paperswithcode.com/paper/antique-a-non-factoid-question-answering)

# Example Use
Notice:
- Before using ANTIQUE dataset, you need to `pip install ir_datasets`. ensure you have installed the required package
  by running pip install ir_datasets. If you encounter any issues with ANTIQUE datasets despite installing ir_datasets,
  please refer to the troubleshooting information provided below.

```python
from RAGchain.benchmark.dataset import AntiqueEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = AntiqueEvaluator(pipeline, evaluate_size=20)
evaluator.ingest(retrievals, db) # ingest dataset to db and retrievals
result = evaluator.evaluate()

# print result summary (mean values)
print(result.results)
# print result DataFrame
print(result.each_results)
```


# Trouble Shooting
### 1. pcre.h File Not Found(MAC OS)

```Bash
ERROR: Could not build wheels for pyautocorpus, which is required to install pyproject.toml-based projects
```

If you have trouble with this error, you need to install the pcre library.<br>
[reference](https://stackoverflow.com/questions/22555561/error-building-fatal-error-pcre-h-no-such-file-or-directory)



### 2. Python.h Missing Error.(MAC OS)

In the case of a missing python.h error, add an environment variable as follows.

```
export CPLUS_INCLUDE_PATH=/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/Headers
export C_INCLUDE_PATH=/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/Headers
```

**For any issues not covered above, please create an issue on our [RAGchain](https://github.com/NomaDamas/RAGchain/issues) GitHub repository!**
