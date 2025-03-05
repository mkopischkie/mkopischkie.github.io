---
title: "Naive Bayes"
permalink: /nb/
layout: single
classes: wide
---

<script type="text/javascript" async
  src="https://polyfill.io/v3/polyfill.min.js?features=es6">
</script>
<script type="text/javascript" async
  id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

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

$$ P(A \mid E) \quad \text{is the posterior, or the probability of A, the response, being true, given that E is true} $$

$$P (E \mid A) \quad \text{is the likelihood, or the probability of the observed variable(s) being true, given A, the response, is true} $$

$$ P(A) \quad \text{is the prior, or how likely the response is true} $$

$$ P(E) \quad \text{is the evidence, or the probability of the evidence being true given all possible responses} $$


Therefore, if we want to find the probability of playing golf given that it is sunny with weak winds, we perform the following calculation.  


$$ P(Yes) = \frac{3}{4} $$

$$ P(No) = \frac{1}{4} $$


$$ P(Sunny | Yes) = \frac{count(Sunny | Yes)}{count(Yes)} = \frac{1}{3} $$

$$ P(Sunny | No) = \frac{1}{1} = 1 $$

$$ P(Weak | Yes) = \frac{count(Weak | Yes)}{count(Yes)} = \frac{2}{3} $$

$$ P(Weak | No) = \frac{0}{1} = 0 $$


$$ P(Yes | Sunny, Weak) = P(Sunny | Yes) * P(Weak | Yes) * P(Yes) = \frac{1}{3} * \frac{2}{3} * \frac{3}{4} = \frac{1}{6} $$

$$ P(No | Sunny, Weak) = P(Sunny | No) * P(Weak | No) * P(No) = 1 * 0 * \frac{1}{4} = 0 $$


The conditional probability formula states that we should divide these results by the evidence term, but the evidence term is the same in both cases so I am not including it in this calculation. This often occurs when using the Naive Bayes algorithm, so we generally ignore that term in the computation. 

$$ P(Yes | Sunny, Weak) > P(No | Sunny, Weak) $$

We conclude that we would play golf given that it is sunny with weak winds. 

I will apply this algorithm to my dataset, combined_data_with_extra_data2.csv, which is a labeled record data dataframe. The label column, 'Golf' in the above example, has to be in the dataset for the probabilities to be calculated. This algorithm requires training and testing data, so I will split my dataframe to 80% training and 20% testing. The model training is necessary in Naive Bayes because without it, the model wouldn't have predetermined probabilities, including the prior, likelihood, and estimate probabilities. If implemented accurately, this algorithm should determine the probability of a particular neurological disorder, given the evidence/features present. 







