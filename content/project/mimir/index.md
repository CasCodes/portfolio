---
title: Mimir - Real-time internet context for claims
summary: Using LangChain and davinci-003 to evaluate claims based on information from the internet in real-time.
tags:
  - ML
date: 2023-04-28
---

> [👉 view on github](https://github.com/unreally-ai/mimir)

## 01 Intro
This project was a follow up to our work on [**Unreally**](https://github.com/VinceDerPrince). [**Vincent**]() and I wanted to build a new fact-checking method using state-of-the-art technologies like LangChain and the OpenAI davinci-003 model.

Our objectives:
1. Extract the key claims of a given text
2. Find relevant internet context and display it in natural language
3. Integrate everything in a web-app

## 02 Design

![mimir pipeline](mimir-pipeline.png)