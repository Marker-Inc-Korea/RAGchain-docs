# LLM

## Overview

RAGchain now use Langchain's LLM LCEL for generating answer. 
Using Langchain LCEL, now you can easily integrate various LLM model to RAGchain easily, without using external OpenAI-like servers.
Plus, it has auto fallback features and stream & async operations. 
You can use whole power of Langchain LCEL with RAGchain.
You can read more about Langchain LCEL at [here](https://python.langchain.com/docs/expression_language/).

And the last thing you must remember, you can always use [`Pipeline`](../../pipeline/README.md), if you don't know about Langchain LCEL or don't want to learn from scratch.
Pipeline is pre-made LCEL runnable for you. You can use it easily. So please check out Pipeline first.

## How to use LCEL at RAGchain

### Basic Usage
You can use `RAGchainPromptTemplate` or `RAGchainChatPromptTemplate` for customize prompt in RAGchain.
You have to include `question` and `passages` in your prompt.
Of course, you can use default Langchain Prompt Templates, too.

The below is simple example.

```python
from operator import itemgetter
from langchain.schema import StrOutputParser
from langchain.schema.runnable import RunnableLambda
from langchain.llms.openai import OpenAI
from RAGchain.schema import Passage
from RAGchain.retrieval import BM25Retrieval

prompt = RAGchainPromptTemplate.from_template("""
    You have to answer question using given passages.
    Question: {question}
    Passages: {passages}
    Answer:""")
bm25_retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")

runnable = {
    "question": itemgetter("question"),
    "passages": itemgetter("passages") | RunnableLambda(lambda x: Passage.make_prompts(bm25_retrieval.retrieve(x))),
} | prompt | OpenAI() | StrOutputParser()

answer = runnable.invoke({"question": "your question"})
```
First, you have to make prompt. Prompt must include `question` and `passages`. You can use another key for question and passages,
but using `question` and `passages` is recommended due to compatibility with RAGchain's other pre-made prompts.
Next, prepare [`Retrieval`](../retrieval/README.md) instance for retrieving passages.
Then, make runnable for running whole pipeline. You can use itemgetter and RunnableLambda for using RAGchain retrieve function in Langchain LCEL.
Lastly, you can invoke runnable with user's question. Then, you can get answer.

### Streaming answers

Streaming answers allows you to receive responses from the LLM model in real-time, as they are generated, rather than
waiting for the entire response to be completed. This can be useful for queries with long passages that may take a while
to generate full responses.

To use this feature, you can use `stream` function of LCEL's runnable. Just replace invoke to stream function.

For example:

```python
prompt = RAGchainPromptTemplate.from_template("""
    You have to answer question using given passages.
    Question: {question}
    Passages: {passages}
    Answer:""")
bm25_retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")

runnable = {
    "question": itemgetter("question"),
    "passages": itemgetter("passages") | RunnableLambda(lambda x: Passage.make_prompts(bm25_retrieval.retrieve(x))),
} | prompt | OpenAI() | StrOutputParser()

for s runnable.stream({"question": "your question"}):
    print(s, end="", flush=True)
```

### 2. Chat History

Chat history is used when you want your model to consider previous interactions while generating a response. 
Of course, you can use `RunnableWithMessageHistory` from Langchain. 

For example:

```python
prompt = RAGchainPromptChatTemplate.from_messages([
        ("system", "You have to answer question using given passages."),
        MessagePlaceholder(variable_name="history"),
        ("user", "Question: {question}\nPassages: {passages}"),
        ("system", "Answer:")
    ])
bm25_retrieval = BM25Retrieval(save_path="your/path/bm25.pkl")

runnable = RunnablePassthrough.assign(
    passages=itemgetter("passages") | RunnableLambda(lambda x: Passage.make_prompts(bm25_retrieval.retrieve(x))),
    question=itemgetter("question"),
)| prompt | OpenAI() | StrOutputParser()
runnable_with_history = RunnableWithMessageHistory(
    runnable,
    lambda session_id: RedisChatMessageHistory(session_id, url="your/redis/url"),
    input_messages_key="question",
    history_messages_key="history"
)

answer = runnable_with_history.invoke({"question": "your question"},
                                       config={"configurable": {"session_id": "your session id"}})
```

### Custom Prompt

A custom prompt is used when you want your model's response based on specific context or information.

You can just simply change your prompt template for custom prompts.

### Custom LLM

Using Custom LLM means using LLM model instead of OpenAI's pre-trained models.
You can easily use all model integrated in Langchain. Full list of integrated models are [here](https://integrations.langchain.com/).
