---
title: "Naive Bayes"
permalink: /nb/
layout: single
classes: wide
---

## Overview 

Naive Bayes is a supervised machine learning technique that operates under Bayes Theorem, also known as conditional probability. It assumes that each feature is independent of one another and calcualtes the probabilities for the desired outcome. A common explanation of the algorithm is shown on a dataset that indicates whether or not to play golf. 

| Outlook  | Wind   | Golf | 
| -------- |------- | ---- | 
| Sunny    | Weak   | Yes  |
| Sunny    | Strong | No   |
| Overcast | Strong | Yes  |
| Overcast | Weak   | Yes  |

The probability of playing golf on a given day can be calculated using Bayes Theorem, or the equation for conditional probability: 

$$ P(A | E) = \frac{P(E | A) P(A)}{P(E)} $$ 

Where, 
- $P(A | E)$ is the posterior, or the probability of A, the response, being true, given that E is true
- $P(E | A)$ is the likelihood, or the probability of the observed variable(s) being true, given A, the response, is true
- $P(A)$ is the prior, or how likely the response is true
- $P(E)$ is the evidence, or the probability of the evidence being true given all possible responses


