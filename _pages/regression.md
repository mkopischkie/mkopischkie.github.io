---
title: "Regression"
permalink: /regression/
layout: single
classes: wide
---

<script type="text/javascript" async src="https://polyfill.io/v3/polyfill.min.js?features=es6"> </script> <script type="text/javascript" async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"> </script>

## Overview 

### Linear Regression 

Linear regression is a parametric, supervised machine learning model. Parametric means that it assumes a linear relationship is present in the data and estimates the parameters of that relationship. The estimation occurs when the model minimizes the distance between the predicted and actual values. Then, it takes the learned relationship and predicts a continuous response. 

### Logistic Regression 

Logistic regression attempts to estimate the parameters of a relationship by minimizing the loss function, which quantifies incorrect predictions. The model returns a binary classification prediction where the predicted values follow a probability distribution, in this case, a Bernoulli distribution, to return a number between zero and one. Using the sigmoid function, the model returns the probability of a sample belonging to a specific class. Generally, the sigmoid function will assign class one if the probability is greater than or equal to 0.5, and class zero otherwise. 

### Similarities/Differences 

Both models are supervised and parametric. Supervised meaning that the model requires a training and testing set, and parametric meaning that a preexisting relationship in the data is assumed. However, linear regression returns a continuous number, whereas logistic regression returns a binary integer. Furthermore, each regression model requires a different data format; linear regression needs to learn on a continous response, such as height or weight, and logistic regression needs to learn on classification labels, such as high, medium, or low (2, 1, 0). 

### Sigmoid Function in Logistic Regression 

The sigmoid function is written as,
$$ f(x) = \frac{1}{1 + e^{-x}} $$ , 
where $x$ is the logit function, a linear combination of all the variables and weights, and is graphically represented below. 

image 

It works by interpreting the logit function, a continuous variable bounded between negative infinity and positive infinity, and transforms it into a probability. The probability is bounded between zero and one and represents the class that the sample most likely belongs to. The class is typically assigned by defining a threshold, so the sigmoid can classify each sample. 

### Maximum Likelihood in Logistic Regression 





