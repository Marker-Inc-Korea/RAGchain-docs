# LLM

## Overview

The LLM module is a tool that generates answers based on a user's given question and retrieved passages. These passages
are fetched by the [`Retrieval`](../retrieval/) module. All LLM modules have their unique features and advantages.
Please read our LLM documentation for further details about each LLM modules.&#x20;

And, many LLM modules supports four additional features: streaming answers, chat history, custom prompts, and custom
LLM. Its usage is same at every LLM modules. But, some LLM module don't support certain features, so please read
supporting feature table below.

## Additional Features

### 1. Stream Answers

Streaming answers allows you to receive responses from the LLM model in real-time, as they are generated, rather than
waiting for the entire response to be completed. This can be useful for queries with long passages that may take a while
to generate full responses.

To use this feature, you must set the `stream` parameter to `True` when calling the `ask` methods. And, you must pass a
function as an argument to the `stream_func` parameter; this function will be called with each chunk of generated text.

When stream is ended, `stream_func` function will be called with `BaseLLM.stream_end_token` so you can easily recognize
generating answer is ended. Default `BaseLLM.stream_end_token` is '<|endofstream|>'.

For example:

```python
from RAGchain.retrieval import BM25Retrieval
from RAGchain.llm.basic import BasicLLM

def stream_func(chunk):
    print(chunk)

retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")
basic_llm = BasicLLM(retrieval, stream_func=stream_func)
basic_llm.ask(query="your question", stream=True)
```

### 2. Chat History

Chat history is used when you want your model to consider previous interactions while generating a response. The history
is automatically included and sent to LLM server when using chat models.

To clear chat history after a conversation has ended or at any required point, call `chat_history` method. For example:

<pre class="language-python"><code class="lang-python"><strong>basic_llm.clear_chat_history()
</strong></code></pre>

### 3. Custom Prompt

A custom prompt is used when you want your model's response based on specific context or information.

We use prompt\_func for using custom prompt. prompt\_func is method that receive retreived passages and user's input
question. You can make custom prompt using user's question and passages, and return custom prompts. Prompts must be
write openai chat messages style. You can see detail
at [openai API documentation](https://platform.openai.com/docs/api-reference/chat/create).

The custom prompt\_func can passed at initialization of LLM module. (if it supports)\
For example:

```python
from typing import List
from RAGchain.schema import Passage
from RAGchain.retrieval import BM25Retrieval
from RAGchain.llm.basic import BasicLLM

def your_prompt_func(query: str, passages: List[Passage]):
    contents = "\n".join([passage.content for passage in passages])
    return [
        {"role": "system", "content": "Answer question using given question"},
        {"role": "user", "content": f"Question: {query}\nPassages: {contents}"}
    ]

retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")
basic_llm = BasicLLM(retrieval, prompt_func=your_prompt_func)
basic_llm.ask(query="your question")
```

### **4. Custom LLM**

Using Custom LLM means using LLM model instead of OpenAI's pre-trained models.

For this purpose, deploy LLM model using open-source projects available for deploying OpenAI style APIs with custom LLM
models. This kind of projects like [vLLM](https://vllm.ai/), [LocalAI](https://github.com/go-skynet/LocalAI), or
oobabooga. Please read our [instruction](./#running-openai-style-server) for running openai-like server with your own
model.

Once deployed successfully, change OpenAI API key and API base according to your deployed server configurations. And,
put model\_name and api\_base when initialize LLM instance.

For example:

```python
import openai
from RAGchain.retrieval import BM25Retrieval
from RAGchain.llm.basic import BasicLLM

openai.api_key = "your-model-name"
openai.api_base = "your-api-base-url"

retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")
basic_llm = BasicLLM(retrieval, model_name="your-model-name", api_base="your-api-base-url")
basic_llm.ask(query="your question")
```

## Supporting Features&#x20;

✅ means the LLM module supports that feature, 🚧 means 'building that feature', and ❌ means the LLM module can't support
that feature.&#x20;

| LLM                             | Stream Answers | Chat History | Custom Prompt | Custom LLM |
|:--------------------------------|:---------------|:-------------|:--------------|:-----------|
| [Basic LLM](basic-llm.md)       | ✅              | ✅            | ✅             | ✅          |
| [Completion LLM](completion-llm.md) | ✅              | ❌             | ✅             | ✅          |

## Running openai-style server

### vLLM

You can check official documentation on vLLM [homepage](https://vllm.ai).

First, install required libraries.

```bash
pip install fschat accelerate vllm
```

Then, run oepnai server with code below.

```bash
python -m vllm.entrypoints.openai.api_server --model <model_name> --port <port_number> --host <host_name>
```

We recommend set host\_name to 0.0.0.0. And you can use any model\_name on huggingface.

### oobabooga

You can use openai extension at
oobabooga. [Here](https://github.com/oobabooga/text-generation-webui/tree/main/extensions/openai) is official
description how to run openai extension of oobabooga. And you can check out how to install
oobabooga [here](https://github.com/oobabooga/text-generation-webui).

More guides are coming soon!
