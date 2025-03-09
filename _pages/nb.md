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


There are various Naive Bayes algorithms to use including: Gaussian, Multinominal, Bernoulli, and Categorical. 
- *Gaussian NB*: works best for dataframes containing continuous features. It assumes that each feature operates under a Gaussian, or normal, distribution. Similar to what I described above, the algorithm determines the maximum posterior probability of a data point and assigns the points to that class. This algorithm performs well on data that already assumes a normal distribution, including house prices or income.
- *Multinominal NB*: works best on discrete data typically used in text mining. It counts the word frequency in documents to classify texts. This algorithm is often used in spam email detection. To estimate the likeliness of a word belonging to a particular class, Multinominal NB uses the maximum likelihood estimator, parametrized by the word frequency, total number of words, and vocabulary size.
- *Bernoulli NB*: is best used on binary data whose features follow the Bernoulli distribution. This algorithm can be implemented for text data that was transformed into binary entries to classify texts or detect spam emails.
- *Categorical NB*: works best with discrete features that belong to a multinomial distribution. Some data sources include surveys or medical charts where the participant answers in categories such as low, medium, or high. Based on the probabilities calculated during training, the algorithm assigns the data point to the class with the highest posterior probabilitiy.


## Data Prep

**Gaussian Naive Bayes** requires continuous data with discrete labels. As the data in my combined_data_with_extra_data2.csv is already continuous, I only need to map the labels to integers and drop the labels from the data. My original data set is pictured below. 

![Orig](/assets/images/combined_df.jpg) 

Then, I split the data into training and testing sets using the train_test_split function from scikit learn. The data I use to perform Gaussian NB is pictured below. 

![Final](/assets/images/final_df_clus.jpg)  

A small snippet of the training set with the corresponding training labels is pictured below: 

| X_train (data)                        | y_train (label)                       |
| ------------------------------------- | ------------------------------------- |
| ![Orig](/assets/images/xtrain_nb.jpg) | ![Orig](/assets/images/ytrain_nb.jpg) | 

Another snippet of the testing set with the corresponding testing labels is pictured below: 

| X_test (data)                        | y_test (label)                       |
| -------------------------------------| ------------------------------------ |
| ![Orig](/assets/images/xtest_nb.jpg) | ![Orig](/assets/images/ytest_nb.jpg) | 


These data sets must be disjoint to ensure proper evaluation. A model cannot be tested on the same data that it was trained on because it would overfit the data. This leads to an inflation in the accuracy and a model that would perform well on the given data, but poorly on unseen data. The next two models also require training and testing sets, but I will leave out the images to avoid redundancy.  

Since **Mulitnominal Naive Bayes** is typically used on text data, I will alter my original dataframe similar to how I did for association rule mining (ARM). By converting each entry to the corresponding column name, I can use this NB method. The text-formatted data is pictured below. 

![Final](/assets/images/trans_data.jpg) 

Now, I can use one-hot-encoding to count the frequency that each bacteria appears in a given sample, so each sample is represented as binary entries. 

![Final](/assets/images/ohe_df.jpg) 

The data preparation for **Categorical Naive Bayes** worked similarly to MN NB. Except as I converted the relative abundances to the column names, I created bins and labels to associate each entry with a high, medium, or low amount of a unique bacteria. I one-hot-encoded this data as well. A snapshot of my data before one-hot-encoding is pictured below. 

![Final](/assets/images/trans_binned_data.jpg) 

## Notes: 
- Each label contains a different number of samples, so I experimented with Random Under Sampler (RUS), Random Over Sampler (ROS), and oversampling with SMOTE. However, each model performed best with no minority/majority class adjustments
- When I refer to building a model with all disorder (overlapping conditions), it means that some samples are diagnosed with Bipolar Disorder and Schizophrenia, while others may be one or the other. So, the unique conditions may be 'Bipolar Disorder, Schizophrenia', 'Bipolar Disorder', 'Schizophrenia' 


## Model Visuals 
- Gaussian NB - all disorders (with overlapping unique conditions)
  ![Final](/assets/images/gaussian_nb_all_data.jpg)
- Gaussian NB - neurodegenerative disorders
  ![Final](/assets/images/gaussian_nb_neuro.jpg)
- Gaussian NB - psychological disorders
  ![Final](/assets/images/gaussian_nb_psych.jpg)


Gaussian Accuracy: 

| Model           | Accuracy |
| --------------- | -------- | 
| All disorders   | 0.8261   |
| Neuro disorders | 0.9688   |
| Psych Disorders | 0.7946   | 


- NM NB - all disorders
  ![Final](/assets/images/mn_nb_all_data.jpg)
- NM NB - neurodegenerative disorders
  ![Final](/assets/images/mn_nb_neuro.jpg)
- NM NB - psychological disorders
  ![Final](/assets/images/mn_nb_psych.jpg)


Multinominal Accuracy: 

| Model           | Accuracy |
| --------------- | -------- | 
| All disorders   | 0.7795   |
| Neuro disorders | 0.9844   |
| Psych Disorders | 0.7407   |


- Categorical NB - all disorders (with overlapping unique conditions)
  ![Final](/assets/images/categorical_nb_full_data.jpg)
- Categorical NB - neurodegenerative disorders
  ![Final](/assets/images/categorical_nb_neuro.jpg)
- Categorical NB - psychological disorders
  ![Final](/assets/images/categorical_nb_psych.jpg)


Categorical Accuracy: 

| Model           | Accuracy |
| --------------- | -------- | 
| All disorders   | 0.8571   |
| Neuro disorders | 0.9688   |
| Psych Disorders | 0.8889   |  




