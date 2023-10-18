---
description: Load various files to RAGchain - compatible with Langchain
---

# File Loader

### Overview

The File Loader is a utility designed to load various files into a List of [`Document`](https://docs.langchain.com/docs/components/schema/document) Objects. It is an integral part of our framework, providing the initial step in processing documents for similarity search using the RAG workflow. This loader is fully compatible with Langchain's [Document Loader](https://python.langchain.com/docs/modules/data\_connection/document\_loaders/) and can be used interchangeably, offering additional special loaders unique to our framework.

### Roles of the File Loader in the Framework

The primary role of the File Loader is to facilitate document ingestion into your application by loading different file types into a standardized List of [`Document`](https://docs.langchain.com/docs/components/schema/document)Objects. Here are some key roles:

1. **Document Ingestion:** The File Loader simplifies document ingestion by accepting various file types and converting them into a unified format ([`Document`](https://docs.langchain.com/docs/components/schema/document) Objects). This makes it easy to handle different kinds of documents within your application.
2. **Compatibility with Langchain's** [**Document Loader**](https://python.langchain.com/docs/modules/data\_connection/document\_loaders/)**:** The File Loader inherits from the same parent class as Langchain's Document loader, ensuring full compatibility between both loaders. You can use either loader based on your specific document file types.
3. **Initial Step in RAG Workflow:** Once documents are loaded via the File Loader, they can be split into passages and converted into vector representations for similarity searches. It is the first step of RAG workflow.

### Advantages of File Loader

The following are some key advantages offered by our File Loaders:

1. **Compatibility with Langchain's** [**Document Loader**](https://python.langchain.com/docs/integrations/document\_loaders)**:** Thanks to its shared inheritance, you get all benefits provided by Langchain’s Document loader along with additional features from our framework's special loaders. You can check out all document loaders from langchain at [here](https://python.langchain.com/docs/integrations/document\_loaders).
2. [**OCR Loaders**](ocr/)**:** Our File Loader includes an OCR (Optical Character Recognition) loader. This allows for the extraction and digitization of text from images or scanned documents, and pdfs. It is useful when you want to ingest complex documents with tables.&#x20;
3. [**HWP Loader**](hwp-loader.md): Recognizing the prevalence and importance of HWP files in South Korea, our File Loader includes a dedicated HWP loader. This ensures seamless loading and processing of one of South Korea's most popular document formats.
4. [**ODQA Dataset Loader**](dataset-loader/)**:** Our File Loaders will support various ODQA dataset loaders, enabling easy ingestion and processing of open-domain question answering datasets for RAG pipeline benchmarking.
