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

### [MSMARCO Dataset](./ms-marco.md)
MSMARCO (Microsoft Machine Reading Comprehension) is a large scale dataset focused on machine reading comprehension, question answering, and passage ranking.
The passages are top-k results Bing engin searched based on question.

### [MrTyDi Dataset](./mr-tydi.md)
Mr.TyDi is a multi-lingual benchmark dataset built on TyDi.
Mr.TyDi apply for languages that is 11 diverse languages and 1 combined diverse languages.

### [BEIR Dataset](./beir.md)
BEIR is a heterogeneous benchmark that has been built from 18 diverse datasets representing 9 information retrieval tasks.
In this project, six datasets are utilized: FEVER, FIQA, HOTPOTQA, QUORA, SCIDOCS, and SCIFACT.

### [Natural Questions Dataset](./natural-question.md)
Natural Questions (NQ) contains real user questions issued to Google search, and answers found from Wikipedia
by annotators. NQ is designed for the training and evaluation of automatic question answering systems.

### [TriviaQA Dataset](./trivia-qa.md)
TriviaQa is a question-answer-evidence triples dataset. Questions-answer pairs are collected 
from 14 trivia and quiz-league websites and evidence are collected from Wikipedia articles and Web search results.

### [NFCorpus](./nfcorpus.md)
NFCorpus is the dataset for Medical Information Retrieval. The queries are  written in non-technical English 
and sourced from the NutritionFacts.org site. Medical documents to retrieve are sourced from PubMed.

### [SearchQA Dataset](./search-qa.md)
The SearchQA question-answer pairs originate from J! Archive2, which comprehensively archives all question-answer pairs
from the renowned television show Jeopardy!

### [ANTIQUE Dataset](./antique.md)
ANTIQUE comprises 2,626 open-domain non-factoid questions sourced from various categories, with a total of 34,011
manually annotated relevance judgments. These questions originated from real users on Yahoo! 
Answers, a community question answering service.

### [ASQA Dataset](./asqa.md)
ASQA (Factoid Questions Meet Long-Form Answers) is the long-form question answering dataset based on ambiguous factoid questions.

### [DSTC11-Track5 Dataset](./dstc11-track5.md)
DSTC11-Track5 is a dataset from the DSTC11-Track5 competition. This dataset is a task-oriented dialogue dataset, 
and the task is to build a dialogue system that assists users in accomplishing specific goals, such as booking a hotel or a restaurant.
