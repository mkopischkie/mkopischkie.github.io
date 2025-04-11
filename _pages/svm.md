---
title: "Support Vector Machine"
permalink: /svm/
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

A Support Vector Machine (SVM) is a supervised, non-parametric, and discriminitive, machine learning model. In other words, it learns from a training set of the data, does not assume any pre-existing relationships, and fits a data vector into a defined category. 

Initially, the algorithm computs the dot product between two vectors to gain insight into how similar the vectors are related. For example, if the dot product between two vectors is zero, the two vectors are perfectly orthogonal, and if the dot product is one, the vectors are perfectly parallel. The dot product is defined as 

$$x \cdot y = \left|\left|x\right|\right| \left|\left|y\right|\right| cos(\theta)$$

where $\theta$ is the angle measured between the two vectors. 

Generally, SVM's try to separate the data with a plane through space. In two or three dimensions, the data may be linearly separable, as depicted in the image below. But often, a linear boundary will not separate the data well, so a non-linear hyperplane is necessary. 

![Orig](/assets/images/svm1.jpg) 





## Data Prep





## Model Evaluation 





## Conclusions
