# OCR

## Overview

The OCR (Optical Character Recognition) File Loader is a powerful tool designed to extract and digitize text from images, scanned documents, and PDFs. It's particularly useful when ingesting complex documents with tables.&#x20;

## Importance of OCR

The Optical Character Recognition (OCR) loader plays a critical role in the Retrieval-Augmented Generation (RAG) workflow. Its primary function is to convert document images, scanned documents, and PDFs into text that can be processed by Large Language Models (LLMs). Here's why the OCR loader is so important:

### 1. Handling Complex Documents

Traditional methods of text extraction might struggle with complex documents, especially those containing tables or a mix of different formats and layouts. The OCR loader is designed to handle such complexity effectively. It uses models to extract text from various document types accurately, expecting high-quality inputs.

### 2. Better Ingestion Leads To Better Answers

The quality of an LLM's responses relies heavily on the quality of its input passages; "garbage in equals garbage out."

By using an OCR loader for file ingestion, you're improving your chances of obtaining accurate and meaningful responses from your LLM because it ensures better recognition and extraction of content from documents.

## Supporting OCR models

1. [Nougat](nougat-loader.md) : Nougat is powerful model for parsing academic document PDF files to mathpix markdown texts, made by Meta. It is great choice to use Nougat when you want to ingest academic paper pdf files.

2. [Deepdoctection](deepdoctection-loader.md) : deepdoctection is a Python library that orchestrates document extraction and document layout analysis tasks using deep learning models. It does not implement models but enables you to build pipelines using highly acknowledged libraries for object detection, OCR and selected NLP tasks and provides an integrated framework for fine-tuning, evaluating and running models. For more specific text processing tasks use one of the many other great NLP libraries.


More models are coming soon!