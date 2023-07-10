---
title: Unreally - Fact-checking bot on Twitter
summary: Unreally is an extendable ecosystem for detecting false claims on social networks. At it's core, we have trained a neural network to perform stance detection on claims.
tags:
  - ML
date: 2022-10-12

---
> [👉 view on github](https://github.com/unreally-ai)

## 01 Intro
We hear a lot about "Fake News" - or disinformation - these days. They are defined as "false information which is inteded to mislead" and can be used in various malicious ways, especially on social media. To manipulate public opinion, distrupt the democratic process or undermine scientific facts.

To spot false claims (e.g. Tweets) on social media, [**Vincent Elster**](https://github.com/VinceDerPrince) and I developed a method using stance detection. Here, we use a neural network to determine the way external context relates to such a claim by classifing their stance as 
- agree (the context agrees with the claim)
- disagree (the context agrees with the claim)
- discuss (the context neutrally discusses the claim)
- unrelated (the context talks about something different)

## 02 Design
There are multiple parts to this projects:
1. Firstly we will create a dataset of claims, context and label (stance)
2. Furthermore we have to find a way to represent these texts numerically in order for the computer to interpret them
3. Then we can build and train a neural network 
4. And finally we will integrate everything into an API and Twitter Bot