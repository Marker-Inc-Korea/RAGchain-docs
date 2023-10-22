# Overview

The DatasetEvaluator classes in the RAGchain framework are used for evaluating metrics using question answering datasets. The datasets currently supported are StrategyQA, Ko-StrategyQA, and Qasper.

# Supporting Datasets

### [StrategyQA Dataset](./strategy-qa.md)

A multi-hop open-domain question answering dataset. It has paragraphs from wikipedia, and every question is multi-hop question, which needs to retrieve multiple paragraphs to answer the question.
Plus, all answers is True/False type. We do not support answer evaluator for this dataset yet. But you can easily check answers by yourself.

### [Ko-StrategyQA Dataset](./ko-strategy-qa.md)

The Korean version of the StrategyQA dataset.

### [Qasper Dataset](./qasper.md)

A dataset for question answering on scientific (NLP) papers. It can evaluate the retrieval performance of one NLP paper document, plus answer performance.
