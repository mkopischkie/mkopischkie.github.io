---
title: "Decision Tree"
permalink: /dt/
layout: single
classes: wide
---

<script type="text/javascript" async src="https://polyfill.io/v3/polyfill.min.js?features=es6"> </script> <script type="text/javascript" async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"> </script>

## Overview 

Decision trees are non-parametric supervised learning model. Non-parametric models do not assume any preexisting relationships in the data, so they can model complex and non-linear relationships. Decision trees are a top-down, greedy algorithm that splits the data into classes until a specified depth is reached. It's easy to think of decision trees as flow charts where each branch represents an answer to a question. 

![dt](/assets/images/dt1.jpg)  

The way that a decision tree is split up is influenced by metrics such as Information Gain and Gini Impurity. Information gain measures how well a question will separate the data. For example, in the image above, one of the questions would be 'Is there a swell?' and the information gain is measured by the split in the answers. There would be a high information gain if, when there was a swell, everyone surfed, and if there isn't a swell, no one would surf. 

The information gain is highly correlated with entropy, which is the measure of randomness and disorder. For instance, if three people surfed when there was no swell and three people did not surf with no swell, the entropy would be high since there is more randomness to decide whether to surf or not. The increase in entropy correlates with a decrease in information gain, since there is not a clear answer to the question asked. 

The Gini Impurity measures the likelihood of misclassification of a data point to a particular category. Therefore, the decision tree algorithm splits the dataset at nodes with the lowest gini impurity. The metric is measured by subtracting the sum of the squared probabilities of a datapoint belonging to a particular class from one. For example, if a sample has an 80% probability of belonging to class 1 and a 20% probability of belonging to class 2, the Gini impurity would be calculated as follows: 

$$ \text{Gini Impurity} = 1 - (0.8^2 + 0.2^2) = 0.32 $$
