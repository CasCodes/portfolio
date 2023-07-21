---
title: Unreally - Fact-checking bot on Twitter
summary: Unreally is an extendable ecosystem for detecting false claims on social networks. At it's core, we have trained a neural network to perform stance detection on claims.
tags:
  - ML
date: 2022-10-12

---
> [👉 view on github](https://github.com/unreally-ai)

We hear a lot about "Fake News" - or disinformation - these days. They are defined as "false information which is inteded to mislead" and can be used in various malicious ways, especially on social media. To manipulate public opinion, distrupt the democratic process or undermine scientific facts.

To spot false claims (e.g. Tweets) on social media, [**Vincent Elster**](https://github.com/VinceDerPrince) and I developed a method using stance detection. Here, we use a neural network to determine the way external context relates to such a claim by classifing their stance as 
- agree (the context agrees with the claim)
- disagree (the context agrees with the claim)
- discuss (the context neutrally discusses the claim)
- unrelated (the context talks about something different)

If you are interested in learning more, you can download our paper below (it's in German).

## Kurzfassung
Um falsche Behauptungen mit Hilfe von maschinellen Lernen zu erkennen ist Stance Detection (SD) eine geeignete Technik, bei der der Standpunkt zwischen einer Behauptung und Nachrichten-Kontext erkannt wird. Daher untersuchen wir verschiedene Methoden zur Integration von Kontext in SD und wie diese sich auf die Leistung eines von uns entwickelten Systems zum Erkennen von Fehlinformationen auswirken.

> [👉 Fehlinformationen durch Kontext erkennen](/uploads/Fehlinformationen_durch_Kontext_erkennen.pdf)