# Token Splitter

## Overview

The `TokenSplitter` is used to split a document into passages by token using various tokenization methods.
It's designed to split text from a document into smaller chunks, or "tokens", using various tokenization methods. 
The class supports tokenization with '`tiktoken`', '`spaCy`', '`SentenceTransformers`', '`NLTK`', and '`huggingFace`'.

The most feature is similar with Langchain's [`Split by token`](https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/split_by_token#tiktoken).

## Usage

The kinds of tokenizer splitters are '`tiktoken`', '`spaCy`', '`SentenceTransformers`', '`NLTK`', and '`huggingFace`'.
The names of splitters are tokenizer name. Each tokenizer tokenizes in a different way.
Its usages are a little bit different.

### Initialization

Here are parameter information. 

- `tokenizer_name`: A tokenizer_name is a name of tokenizer. You can choose tokenizer_name.<br>
(tiktoken, spaCy, SentenceTransformers, NLTK, huggingFace)
- `chunk_size`: Maximum size of chunks to return. Default is 100.
- `chunk_overlap`: Overlap in characters between chunks. Default is 0.
- `pretrained_model_name`: A huggingface tokenizer pretrained_model_name to use huggingface token splitter.
You can choose various pretrained_model_name in this parameter. Default is "gpt2".
Refer to pretrained model in this link.  (https://huggingface.co/models)
- `kwargs`: Additional arguments.

We offer to `sample_test_document.txt` for test. 
If you want to use our test file, try this code!

```Python
import os
import pathlib

root_dir = pathlib.PurePath(os.path.dirname(os.path.realpath(__file__))).parent.parent.parent
file_path = os.path.join(root_dir, "resources", "sample_test_document.txt")

with open(file_path) as f:
    state_of_the_union = f.read()

TEST_DOCUMENT = Document(
    page_content=state_of_the_union,
    metadata={
        'source': 'test_source',
        'Data information': '맨까 새끼들 부들부들하구나',
        'What is it?': 'THis is token splitter'
    }

```

### Tiktoken

First, initialize an instance of `TokenSplitter` and input tokensplitter.

```Python
from RAGchain.preprocess.text_splitter import TokenSplitter

tiktoken = TokenSplitter(tokenizer_name='tiktoken', chunk_size=1000, chunk_overlap=0)
```


### Split document(tiktoken)

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
tiktoken_passages = tiktoken.split_document(TEST_DOCUMENT)
```

### spaCy

To use spaCy token splitter, you should install some packages.

```Python
!python -m spacy download en_core_web_sm
!pip install spaCy
```

Initialize an instance of TokenSplitter and input parameter `tokenizer_name=spaCy`.

```Python
from RAGchain.preprocess.text_splitter import TokenSplitter

spaCy = TokenSplitter(tokenizer_name='spaCy', chunk_size=1000, chunk_overlap=0)
```

### Split document(spaCy)

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
spaCy_passages = spaCy.split_document(TEST_DOCUMENT)
```


### SentenceTransformers

Initialize an instance of TokenSplitter and input parameter `tokenizer_name=SentenceTransformers`.

```Python
from RAGchain.preprocess.text_splitter import TokenSplitter

sentence_transformers = TokenSplitter(tokenizer_name='SentenceTransformers', chunk_overlap=0)
```

### Split document(SentenceTransformers)

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
SentenceTransformers_passages = sentence_transformers.split_document(TEST_DOCUMENT)
```


### NLTK

Initialize an instance of TokenSplitter and input parameter `tokenizer_name=NLTK`.
To use NLTK token splitter, you should install some packages.

```Python
!pip install NLTK
```

```Python
from RAGchain.preprocess.text_splitter import TokenSplitter

NLTK = TokenSplitter(tokenizer_name='NLTK', chunk_size=1000)
```
### Split document(NLTK)

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
NLTK_passages = NLTK.split_document(TEST_DOCUMENT)
```

#### Trouble Shooting(NLTK)

##### 1. Lookup error

If you occur `Lookup Error`, Try this code! This error occurs because some NLTK files have not been downloaded.

```Python
import nltk
nltk.download('all')
```

[Reference](https://stackoverflow.com/questions/35861482/nltk-lookup-error)


### HuggingFace
> HuggingFace splitter 

AutoTokenizer of huggingface transformer makes you can choose various huggingface's pretrained models. (Refer to this [link](https://huggingface.co/models)!)
Default pretrained model is `gpt2`.

```Python
from RAGchain.preprocess.text_splitter import TokenSplitter

huggingFace = TokenSplitter(tokenizer_name='huggingFace', chunk_size=100, chunk_overlap=0, pretrained_model_name= "gpt2")
```

### Split document(HuggingFace)

You can split document using `split_document()` method. It will return list of [`Passage`](https://nomadamas.github.io/RAGchain/build/html/RAGchain.schema.html#module-RAGchain.schema.passage) objects. For example:

```Python
huggingface_passages = huggingFace.split_document(TEST_DOCUMENT)
```

<br>
<br>

**Notice**:
All tokenizer refer to langchain's library. 
If you want to know more tokenizer information, Refer to this link for more information. 
<br> 
[split by token](https://python.langchain.com/docs/modules/data_connection/document_transformers/text_splitters/split_by_token#tiktoken)