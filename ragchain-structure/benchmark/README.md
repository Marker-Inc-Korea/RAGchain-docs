---
description: Evaluate your pipeline
---

# Benchmark

## Overview

The RAGchain `Benchmark` Module is a tool designed for the evaluation of Retrieval-Augmented Generation (RAG) workflows.
It allows developers to evaluate their pipelines performance with different datasets and user's questions.

## Supporting Evaluators

The `Benchmark` module supports two types of evaluators: AutoEvaluator and DatasetEvaluator.

- **AutoEvaluator:** This tool allows you to evaluate your pipeline with your own questions without a dataset. It can
  evaluate retrieved passages and answers without ground truth answers and ground truth retrieved passages.

- **DatasetEvaluator:** This tool can evaluate your pipeline with question answering datasets.
  

## Supporting Datasets
- [StrategyQA](https://allenai.org/data/strategyqa)
- [Ko-StrategyQA](https://huggingface.co/datasets/NomaDamas/Ko-StrategyQA)
- [Qasper](https://allenai.org/data/qasper)
- [MS-MARCO](./dataset-evaluator/ms-marco.md)
- [Mr-Tydi](./dataset-evaluator/mr-tydi.md)

## Supporting Metrics

Each evaluator supports different metrics.
Default metrics is basically running metrics if you run test file.
Support metrics is the metrics you are available.
This separation is because Ragas metrics take a long time in evaluation.

✅ means that the evaluator supports the metric.
❌ means that the evaluator does not support the metric.
🚧 means that the evaluator will support the metric in the future.
(D) refer to default metrics
(S) refer to support metrics

|                                | [AutoEvaluator](./auto-evaluator.md) | [Qasper](./dataset-evaluator/qasper.md) | [Ko-Strategy-QA](./dataset-evaluator/ko-strategy-qa.md) | [Strategy-QA](./dataset-evaluator/strategy-qa.md) | [ms-marco](./dataset-evaluator/ms-marco.md) | [mr-tydi](./dataset-evaluator/mr-tydi.md) | [beir](./dataset-evaluator/beir.md) |
|:------------------------------:|:------------------------------------:|:---------------------------------------:|:-------------------------------------------------------:|:-------------------------------------------------:|:-------------------------------------------:|:-----------------------------------------:|:-----------------------------------------:|
|            AP  (D)             |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|           NDCG  (D)            |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|            CG  (D)             |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|          Ind_DCG  (D)          |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|           IDCG  (D)            |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|          Recall  (D)           |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|         Precision  (D)         |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|            RR  (D)             |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ❌                      |
|           Hole  (D)            |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|         Accuracy  (D)          |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|            EM  (D)             |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|            F1  (D)             |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|   ragas context-recall  (S)    |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|  ragas context-precision  (S)  |                  ✅                   |                    ✅                    |                            ✅                            |                         ✅                         |                      ✅                      |                      ✅                      |                      ✅                      |
|  ragas answer-relevancy  (S)   |                  ✅                   |                    ✅                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ✅                      |
|    ragas faithfullness  (S)    |                  ✅                   |                    ✅                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ✅                      |
|           BLEU  (D)            |                  ❌                   |                    ✅                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ✅                      |
|          ROUGE-L  (D)          |                  🚧                  |                   🚧                    |                           🚧                            |                        🚧                         |                     🚧                      |                      🚧                      |                      ❌                      |
|           KF1  (D)             |                  ❌                   |                    ✅                    |                            ❌                            |                         ❌                         |                      ✅                      |                      ❌                      |                      ✅                      |

## Role of the Evaluator in the Framework

The `Benchmark` module evaluate the performance of the RAG workflow by generated answers and retrieved passages. The
performance is measured using more than 10 metrics. The evaluators provide a holistic view of the model's performance
and help in identifying areas of improvement.

## Advantages of Evaluators

- **Comprehensive Evaluation:** The evaluators provide a thorough and detailed evaluation of the RAG workflow. They
  assess the performance of the workflow from multiple aspects and provide a comprehensive view of its effectiveness.

- **Flexible:** They allow you to use your own questions or question answering datasets for evaluation. Plus, you can
  create your own Evaluator for new datasets.

- **Easy to Use:** The evaluators come with an easy-to-use interface. You just need to provide your pipeline, and the
  evaluators will take care of the rest. You even don't have to download the datasets. The evaluators will download the
  dataset automatically.
