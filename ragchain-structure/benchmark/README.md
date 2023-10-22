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

- **DatasetEvaluator:** This tool can evaluate your pipeline with question answering datasets. It currently
  supports [StrategyQA](https://allenai.org/data/strategyqa)
  dataset, [Ko-StrategyQA](https://huggingface.co/datasets/NomaDamas/Ko-StrategyQA) dataset,
  and [Qasper](https://allenai.org/data/qasper) dataset.

## Supporting Metrics

Each evaluator supports different metrics.

✅ means that the evaluator supports the metric.
❌ means that the evaluator does not support the metric.
🚧 means that the evaluator will support the metric in the future.

|                         | [AutoEvaluator](./auto-evaluator.md) | [Qasper](./dataset-evaluator/qasper.md) | [Ko-Strategy-QA](./dataset-evaluator/ko-strategy-qa.md) | [Strategy-QA](./dataset-evaluator/strategy-qa.md) |
|:-----------------------:|:------------------------------------:|:---------------------------------------:|:-------------------------------------------------------:|:-------------------------------------------------:|
|           AP            |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|          NDCG           |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|           CG            |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|         Ind_DCG         |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|          IDCG           |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|         Recall          |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|        Precision        |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|           RR            |                  ❌                   |                    ❌                    |                            ❌                            |                         ❌                         |
|          Hole           |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|        Accuracy         |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|           EM            |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|           F1            |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
|  ragas context-recall   |                  ❌                   |                    ✅                    |                            ✅                            |                         ✅                         |
| ragas context-precision |                  ✅                   |                    ✅                    |                            ✅                            |                         ✅                         |
| ragas answer-relevancy  |                  ✅                   |                    ✅                    |                            ❌                            |                         ❌                         |
|   ragas faithfullness   |                  ✅                   |                    ✅                    |                            ❌                            |                         ❌                         |

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
  evaluators will take care of the rest. You even don't have to download the datasets. The evaluators will download the dataset automatically.
