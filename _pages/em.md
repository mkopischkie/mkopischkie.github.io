---
title: "Emsemble Learning"
permalink: /em/
layout: single
classes: wide
---

## Overview 

Ensemble learning involves using multiple algorithms to learn and improve off each other. The main concepts in ensemble learning are bagging, boosting, and stacking. 

### Bagging 

In general, bagging is used to reduce the variance in a noisy dataset. Also known as bootstrap aggregation, the algorithm randomly samples the data with replacement, trains the model on each sample, and stores the accuracy. The final accuracy reported is calculated by taking the average, or majority scores. Often, the accuracy estimates from bagging are higher than without ensemble learning. On the downside, its harder to interpret bagging algorithms due to the average, or majority, accuracy score. 

Random Forests are somewhat of a combination between decision trees and bagging. They randomly sample the rows with replacement (bootstrap), and randomly sample the features. The result is a subset of the rows and a subset of the columns that train many decision trees. By sampling the features, random forests can measure the feature importance with more accuracy than decision trees and prevent overfitting. 

### Boosting

A boosting algorithm creates a strong learner, from a set of weak learners, to minimize classification errors. These models learn sequentially and adjust the weight of the errors from any previous misclassifications. The end classifier has properly distributed weights to minimize the odds of misclassification. Some examples include AdaBoost, Gradient Boosting, and XGBoost. 

### Stacking 

Different from bagging or boosting, stacking uses two or more different models to make predictions. There are base models and a meta model. The base models make prediction on part of the training data and these predictions are fed as inputs to the meta model. The meta model learns to combine the predictions to make the final output.  
 


## Data Prep 





## Model Evaluation 





## Conclusions
