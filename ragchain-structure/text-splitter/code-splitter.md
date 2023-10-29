# Code Splitter

## Overview

The `CodeSplitter` class in the RAGchain library is a text splitter that splits documents based on separators of langchain's library Language enum.
This class inherits from the `BaseTextSplitter` class and uses the from_language method of `RecursiveCharacterTextSplitter` class from the langchain library to perform the splitting. <br>
Reference([Split code](https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter))

`CodeSplitter` supports `CPP`, `GO`, `JAVA`, `KOTLIN`, `JS`, `TS`, `PHP`, `PROTO`, `PYTHON`, `RST`, `RUBY`, `RUST`, `SCALA`, `SWIFT`, `MARKDOWN`, `LATEX`, `HTML`, `SOL`, `CSHARP`.


## Usage

### Initialization

First, to initialize an instance of `CodeSplitter`, you can provide the following parameters: <br>

- `language_name`: A kind of language to split. Default is PYTHON.<br>
  (CPP, GO, JAVA, KOTLIN, JS, TS, PHP, PROTO, PYTHON, RST, RUBY, RUST, SCALA, SWIFT, MARKDOWN, LATEX, HTML, SOL, CSHARP)
- `chunk_size`: Maximum size of chunks to return. Default is 50. 
- `chunk_overlap`: Overlap in characters between chunks. Default is 0.
- `kwargs`: Additional arguments to pass to the langchain RecursiveCharacterTextSplitter.

Let's take a look example how code splitter split `document`s in various language.

Notice: You can't indent TEST_DOCUMENT for legible. Splitter recognize indent and space. Input raw data not space or indent.

### PYTHON

First, initialize an instance of `CodeSplitter`. For example:

```Python
from RAGchain.preprocess.text_splitter import CodeSplitter

code_splitter = CodeSplitter(language_name= 'PYTHON', chunk_size= 50, chunk_overlap= 0)
```

### Split document

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
python_doc = Document(
page_content="""
def hello_world():
    print("Hello, World!")

# Call the function
hello_world()
""",
    metadata={
        'source': 'test_source',
        # Check whether the metadata_etc contains the multiple information from the TEST DOCUMENT metadatas or not.
        'Data information': 'test for python code document',
        'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#python'
    }
)

passages = code_splitter.split_document(python_doc)
```
```
[Passage(id=UUID('8657860f-9a9f-412e-82dd-4fa53d59a893'), content='def hello_world():\n    print("Hello, World!")', filepath='test_source', next_passage_id=UUID('661fd986-4303-4e13-b645-83ab1c183b72'), metadata_etc={'Data information': 'test for python code document', 'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#python'}), 
Passage(id=UUID('661fd986-4303-4e13-b645-83ab1c183b72'), content='# Call the function\nhello_world()', filepath='test_source', previous_passage_id=UUID('8657860f-9a9f-412e-82dd-4fa53d59a893'), metadata_etc={'Data information': 'test for python code document', 'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#python'})]
```

<br>
<br>
<br>

### JS

Process is same as python splitter above. Input language_name JS.

```Python
from RAGchain.preprocess.text_splitter import CodeSplitter

code_splitter = CodeSplitter(language_name= 'JS', chunk_size= 60, chunk_overlap= 0)
```

### Split document

```python
JS_doc = Document(
page_content="""
function helloWorld()
{
    console.log("Hello, World!");
}

// Call the function
helloWorld();
""",
metadata={
    'source': 'test_source',
    # Check whether the metadata_etc contains the multiple information from the TEST DOCUMENT metadatas or not.
    'Data information': 'test for js code document',
    'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#js',
}
)

passages = code_splitter.split_document(JS_doc)
```
```
[[Passage(id=UUID('bb994a5b-15cf-4d8c-a8fc-43584662fd4a'), content='function helloWorld()\n{\n    console.log("Hello, World!");\n}', filepath='test_source', next_passage_id=UUID('128ef1f2-dd79-44cc-8a66-66ed3a5aeb55'), metadata_etc={'Data information': 'test for js code document', 'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#js'}), 
Passage(id=UUID('128ef1f2-dd79-44cc-8a66-66ed3a5aeb55'), content='// Call the function\nhelloWorld();', filepath='test_source', previous_passage_id=UUID('bb994a5b-15cf-4d8c-a8fc-43584662fd4a'), metadata_etc={'Data information': 'test for js code document', 'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#js'})]
```

<br>
<br>
<br>

### C#

Process is same as python splitter above. Input language_name JS.

```Python
from RAGchain.preprocess.text_splitter import CodeSplitter

code_splitter = CodeSplitter(language_name= 'CSHARP', chunk_size= 17, chunk_overlap= 0)
```

### Split document

```python
csharp_doc = Document(
page_content="""
using System;
class Program
{
    static void Main()
    {
        int age = 30; // Change the age value as needed

        // Categorize the age without any console output
        if (age < 18)
        {
            // Age is under 18
        }
        else if (age >= 18 && age < 65)
        {
            // Age is an adult
        }
        else
        {
            // Age is a senior citizen
        }
    }
}
"""
    ,
    metadata={
        'source': 'test_source',
        # Check whether the metadata_etc contains the multiple information from the TEST DOCUMENT metadatas or not.
        'Data information': 'test for C# text document',
        'Data reference link': 'https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/code_splitter#c',
    }
)

passages = code_splitter.split_document(csharp_doc)
```

-> C# `code splitter` splits into 33 passages.

