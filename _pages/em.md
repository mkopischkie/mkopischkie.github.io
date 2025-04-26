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

![kmeans](/assets/images/bagging.jpg) 

Random Forests are somewhat of a combination between decision trees and bagging. They randomly sample the rows with replacement (bootstrap), and randomly sample the features. The result is a subset of the rows and a subset of the columns that train many decision trees. By sampling the features, random forests can measure the feature importance with more accuracy than decision trees and prevent overfitting. 

### Boosting

A boosting algorithm creates a strong learner, from a set of weak learners, to minimize classification errors. These models learn sequentially and adjust the weight of the errors from any previous misclassifications. The end classifier has properly distributed weights to minimize the odds of misclassification. Some examples include AdaBoost, Gradient Boosting, and XGBoost. 

![kmeans](/assets/images/boosting.jpg) 

### Stacking 

Different from bagging or boosting, stacking uses two or more different models to make predictions. There are base models and a meta model. The base models make prediction on part of the training data and these predictions are fed as inputs to the meta model. The meta model learns to combine the predictions to make the final output.  
 
![kmeans](/assets/images/stacking.jpg) 

## Data Prep 

Random Forests, similar to Decision Trees, require the same data format. They handle continuous, and categorical variables, mapped to integers, very well. I fit the random forest model to a dataframe with all the neurological conditions and to another dataframe with only the neurodegenerative conditions. The neurodegenerative conditions were able to maintain the Sex and Age columns, so I remapped the Sex column to binary integers. Then, I could split my data into training and testing sets. The training data emcompassed 80% of the data. The training and testing sets must be mutually exclusive because if a model sees the same data it was trained on, it will overfit, inflate the accuracy, and perform poorly on new data. 

Before transformations, my dataframe is pictured below. 

![Orig](/assets/images/combined_df.jpg) 

After transformations for all the neurological disorders, my dataframe is pictured below. 

![Orig](/assets/images/dt_alldata.jpg) 

After transformations for the neurodegenerative disorders, my dataframe is pictured below.

![Orig](/assets/images/dt_neuro.jpg) 

Next, I performed XGBoost on both dataframes mentioned above. XGBoost also works best on continuous features and can handle binary or multiclass classification. Because of this, I used the same data transformations as above to model all the neurological disorders and the neurodegenerative disorders. Attached below are images of my training and testing sets for the neurological dataframe. Please note that the dataframe for neurodegenerative disorder would look similar, but would have Sex and Age as columns. The splits may not be the exact same due to random selection, but the format would look the same.  

| X_train (data)                        | y_train (label)                       |
| ------------------------------------- | ------------------------------------- |
| ![Orig](/assets/images/x_train_dt.jpg) | ![Orig](/assets/images/y_train_dt.jpg) | 

| X_test (data)                        | y_test (label)                       |
| -------------------------------------| ------------------------------------ |
| ![Orig](/assets/images/x_test_dt.jpg) | ![Orig](/assets/images/y_test_dt.jpg) | 



## Model Evaluation 

1. Random Forest w/ all data
   ![Orig](/assets/images/rf_alldata_graphs.jpg)

2. Random Forest Neurodegenerative
   ![Orig](/assets/images/rf_neuro_graphs.jpg)

3. XGBoost w/ all data
   ![Orig](/assets/images/xgb_alldata_graphs.jpg)
   ![Orig](/assets/images/xgb_feature_importance.jpg)

4. XGBoost Neurodegenerative
   ![Orig](/assets/images/xgb_neuro_graphs.jpg)
   ![Orig](/assets/images/xgb_neuro_feature_importance.jpg)

Accuracies: 

| Model | Accuracy | 
|-------|----------|
| RF w/ all data | 0.9255 |
| RF w/ neuro | 1.0 |
| XGBoost w/ all data | 0.9193 |
| XGBoost w/ neuro | 0.9688 | 


## Conclusions
