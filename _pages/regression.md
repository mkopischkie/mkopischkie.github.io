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

![Orig](/assets/images/log_lin.jpg)  

### Sigmoid Function in Logistic Regression 

The sigmoid function, pictured below, depends on the logit function, a linear combination of all the variables and weights. 

![Orig](/assets/images/sigmoid.jpg)  

It works by interpreting the logit function, a continuous variable bounded between negative infinity and positive infinity, and transforms it into a probability. The probability is bounded between zero and one and represents the class that the sample most likely belongs to. The class is typically assigned by defining a threshold, so the sigmoid can classify each sample. 

### Maximum Likelihood in Logistic Regression 

The maximum likelihood function maximizes the likelihood and log-likelihood equations that are derived from the sigmoid function. This essentially ensures that each sample is either as close to one or as close to zero probability as possible. The algorithm does this by taking the partial derivatives of the log-likelihood functions, dependent on the sigmoid function which is dependent on the original linear combination of features in the model, and setting it equal to zero. In logistic regression, this solution works out nicely where the maximum likelihood function is optimizing the actual value of y, subtracted from the predicted value of y, and the quantity multiplied by the features' weight. 


## Data Prep

Initially, I performed Logistic Regression on a numerical dataframe between the Healthy class and the Parkinsons class. Logistic Regression requires numerical, either float or integer, data types, and in this case, a binary classification label. Using the data from the final_df.csv file, I removed the unecessary conditions, apart from Health and Parkinsons. Then, I removed the Country and BMI columns, deleted any row with Age less than or equal to one, and mapped the male and female sex's to one and zero, respectively. Therefore, I was left with the Condition, or label, column, Sex, Age, and the bacterial genus' columns. 

![Orig](/assets/images/log_reg_origdf.jpg)  

To perform logistic regression, I split my data and kept 80% as the training and 20% as the testing set. Experimenting with my code, I found that the highest accuracy was achieved when I used an oversampling technique, SMOTE. SMOTE creates synthetic training data in the minority class so that the length of the minority and majority classes are equal. In this case, the algoirhtm created data to add to the Parkinsons class to match the length of the Health class. It is important to note that the oversampling is only performed on the training data and not the testing data. 

Per the instructions, I created another model that uses the same data frame that is used in Multinomial Naive Bayes. Again, I tested between the Health and Parkinsons classes, but dropped the columns that were not the bacterial genus'. 

![Final](/assets/images/final_df_clus.jpg) 

I saved the label and dropped it from the dataframe berfore performing the following steps. Multinomial Naives Bayes performs best on text data, so I transformed the above data frame by replacing any entry greater than zero with the column name. For better organization, I wanted the non-zero entries in the leftmost columns. So, I transformed the data into a list, dropped the NANs, and put the list back into a dataframe, replacing the NANs with zeros. Finally, I one-hot-encoded the dataframe so that the unique bacteria names became the column names, and the samples had ones or zeros under each column to represent as to whether the sample contained that bacteria or not, respectively. 

![Final](/assets/images/logreg_mnnb.jpg) 

I split the data into training and testing sets using the same proportions as above. Then, I continued to perform both logistic regression and multinomial naive bayes on the same dataframe to compare the results. 

## Model Evaluation 

The first model I tested used the data with float decimals with the classes Health and Parkinsons. This Logistic Regression model obtained an accuracy of **0.8704** and is pictured below. 

![Final](/assets/images/log_reg_health_park.jpg) 

The next models used the same data from multinomial naive bayes (text data). In other words, the data is binary, indicating the presense of bacteria, or lack thereof. The logistic regression model with this data type obtained an accuracy of **1.0** and is pictured below. This accuracy may be misleading and I will discuss the implications in the next section. 

![Final](/assets/images/log_reg_health_park_mnnb.jpg) 

I compared the above linear regression model to the multinomial naive bayes algorithm. Again, the accuracy is **1.0** and is pictured below. 

![Final](/assets/images/mn_nb_health_park.jpg) 


## Conclusions

The perfect accuracy from the models using text data may be due to several reasons. 

1. A feature that is only present in one class and not the other. To visually support this, I created a boxplot and attached it below. I expect that the presence of a bacterial genus will not be constant across all individuals with unique neurological disorders. But, I believe the one-hot-encoding that was necessary to create the text data may have made these differences too contrasting.
  ![Final](/assets/images/boxplots_sanitycheck.jpg)
2. The taxonomy names may be unique to each condition. Over the past decade, the scientific names of bacteria have changed, even though they mean the same thing. For example, Escherichia coli was previously named Bacteriun coli. If the Health class calls it Bacteriun coli and the Parkinsons class calls it Escherichia coli, the algorithm will learn this pattern and automatically classify a sample based on this bacterium.
3. Overfitting. The dataframe I used to perform these algorithms contained about 200 rows, which is likely too small to represent the entire population of healthy individuals and those with Parkinsons. In this case, if the algorithm is introduced to new data, it may not recognize the correct pattern and can misclassify it.
4. Imbalanced data. The healthy class has about 100 more entries than the Parkinsons class, so the imbalanced classes may be affecting the algorithm. To address this, I tried using Random Over Sampling and SMOTE, to add more entries to the minority class, but neither had an affect on the accuracy. I also tried L1/L2 regularization and the elastic net combination, but still neither affected the accuracy. 

The first model, using float point numerical data performed more reasonably and still gave a great accuracy. Since I did not see a perfect accuracy here, I don't believe there to be any features that are only present in one class and not the other. This leads me to believe that the second and third reasons for the perfect accuracy are the most likely. 









