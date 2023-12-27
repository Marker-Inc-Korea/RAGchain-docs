# Overview

NFCorpus is a comprehensive English full-text retrieval dataset designed for Medical Information Retrieval. 
The dataset comprises 3,244 natural language queries, written in non-technical English and sourced from the 
NutritionFacts.org site. It includes 169,756 automatically extracted relevance judgments for 9,964 medical documents, 
characterized by a complex and terminology-heavy language, primarily sourced from PubMed.<br>
Further information about NFCorpus, please visit below website.

[nfcorpus ir_datasets](https://ir-datasets.com/nfcorpus.html)<br>
[Homepage](https://www.cl.uni-heidelberg.de/statnlpgroup/nfcorpus/)<br>
[Paper](https://link.springer.com/chapter/10.1007/978-3-319-30671-1_58)

# Example Use
Notice:
- Before using NFCorpus dataset, you need to `pip install ir_datasets`. ensure you have installed the required package 
by running pip install ir_datasets. If you encounter any issues with nfcorpus datasets despite installing ir_datasets, 
please refer to the troubleshooting information provided below. 

```Python
from RAGchain.benchmark.dataset import NFCorpusEvaluator

pipeline = <your pipeline>
retrievals = [<your retrieval>]
db = <your db>

evaluator = NFCorpusEvaluator(pipeline, evaluate_size=20)
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
