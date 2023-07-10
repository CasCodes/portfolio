---
title: Mimir - Real-time internet context for claims
summary: Using LangChain and davinci-003 to evaluate claims based on information from the internet in real-time.
tags:
  - ML
date: 2023-04-28
---

> [👉 view on github](https://github.com/unreally-ai/mimir)

## 01 Intro
This project was a follow up to our work on [**Unreally**](https://github.com/unreally-ai). [**Vincent**](https://github.com/VinceDerPrince) and I wanted to build a new fact-checking method using state-of-the-art technologies like LangChain and the OpenAI davinci-003 model.

Our objectives:
1. Extract the key claims of a given text
2. Find relevant internet context and display it in natural language
3. Integrate everything in a web-app

## 02 Design 📝
For the first objective, we are using TextRank + Bert. TextRank is a graph-based algorithm that performs extrative summarization, meaning is boils down a given text to its most important words or sentences without paraphrasing or altering them.

While this gives us the key sentences of the text, we still need a way to determine which of these are actually claims. This is done by using the BERT ClaimBusters model from Huggingface, which classifies each sentence from the summarization as claim or non-claim, leaving us with a list of the top-k key claims.

![mimir pipeline](mimir-pipeline.png)

All of this is passed into a LangChain pipeline. First we use the integrated Google search API to find relevant web context for these claims and then scrape the text. 
The texts and the claims are used to prompt davinci to determine whether the context agrees with the claims or not. 
We use prompt enigneering techniques to achieve a neutral answer that includes both pros and cons:

```python
# 💡 Info: We use few-shot prompting, meaning we give examples first
prompt = f"""
    claim: Exercise is good for mental health.
    context: Research studies have consistently shown that physical exercise can help reduce symptoms of anxiety and depression.
    answer: The found context agrees with the claim, since exercise can help reduce symptoms of anxiety.

    claim: Video games are a waste of time.
    context: Many people enjoy playing video games as a form of entertainment and social interaction. However, videogames are linked to procrastination.
    answer: The found context partially agrees with the claim, since some people enjoy videogames but it might lead to procrastination.

    claim: {query}

    Provide an Answer to the last given claim as demonstrated in the above examples and based on the context below.
    """
# 💡 Info: The internet context will be appended below to the prompt
```

This leads to differentiated answers, e.g. for the claim _"Running is bad for your health"_ :
> While running can be beneficial to your health, too much running can lead to chronic injuries, abnormal heartbeats and other health risks.

Finally, the answer and all the sources used for context are displayed in an UI. We've designed it to be clean and minimal in Figma and then implemented everything as a web-app using Pythons Flask library.
You have the option to either upload a document or get context for a single claim. Once the orange button is pressed, the program will start. 

![mimir ui](mimir-ui.png)

## Closing Thoughts 💭
There are multiple use cases for a system that gathers and interprets internet context in real-time:
- When training other machine learning models, this system could augment text data
- Automated fact-checking like we did with [**Unreally**](https://github.com/unreally-ai) often requires the latest relevant news to work in production
- It can be integrated into other application to improve the users text understanding (e.g. for education or scientific research)

While our LangChain system already works well for these use cases, there are some parts of the pipeline which need improvement. In particular, the claim-extraction with TextRank + BERT has a lot of false positives. This means that the model classifies most sentences as claims, which is unsurprising because what exactly is a claim anyways?
A way to narrow down the criteria for claims could be to only focus on political and economic claims by fine-tuning the model further in the future.

