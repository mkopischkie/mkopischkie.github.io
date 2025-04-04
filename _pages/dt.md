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

The Gini Impurity measures the likelihood of misclassification of a data point to a particular category. Therefore, the decision tree algorithm splits the dataset at nodes with the lowest gini impurity. The metric is measured by subtracting the sum of the squared probabilities of a datapoint belonging to a particular class from one. For example, if the algorithm is determining which node to split the data at, and one sample has an 80% probability of belonging to class 1 and a 20% probability of belonging to class 2, the Gini impurity would be calculated as follows: 

$$ \text{Gini Impurity} = 1 - (0.8^2 + 0.2^2) = 0.32 $$

If, at the other node, the same sample has a 70% probabilitiy of belonging to class 1 and a 30% probability of belonging to class 2, the Gini impurity would be 0.45. Therefore, the algorithm would split the data at the first node which has the lower Gini impurity. 

Decision trees have many practical applications in strategy formulation, risk assessment, customer segmentation, and medical diagnositcs. Here, I hope to use decision trees to predict/classify the samples to the corresponding neurological disorder. 

![dt](/assets/images/dt2.jpg)  

## Data Prep

Numerical data types are required for decision tree performance. Any categorical data types need to be transformed before running the model. To analyze a decision tree with all the data I collected in my combined_data_with_extra_data2.csv, I dropped all the columns besides the bacterial genuses. I needed to do this because some disorders didn't contain the relevant information including Age, BMI, or Sex. By dropping the rows without entries in these columns, I would lose individual disorders, such as Depression, all together. Before making any changes, my dataframe looked like this: 

![Orig](/assets/images/combined_df.jpg)  

After making changes to model a decision tree with all my data, my dataframe looked like this: 

![Orig](/assets/images/dt_alldata.jpg) 

Then I split my data into a training and testing set and modeled the decision tree. The training and testing dataframes looked similar to the snapshots provided in the Naive Bayes tab. Where X_train is the data used and y_train are the corresponding labels. Each model has a unique training and testing dataframe that may be composed of more columns, including Age, BMI, or Sex, and will most likely have different rows of the data due to the random sampling of the train_test_split command. Again, the training and testing dataframes are disjoint due to the reasons listed in the Naive Bayes tab. 

Next, I wanted to model the neurodegenerative disorders, so I filtered my original dataframe to keep only the Parkinson's, Alzheimers, and Health conditions. In this new dataframe, all the samples containing these disorders had entries for Sex and Age. To keep these attributes, I mapped Sex to numerical labels and removed the rows with an Age less than one. My final neurodegenerative disorder dataframe looks like this: 

![Orig](/assets/images/dt_neuro.jpg) 

I also wanted to model the psychological disorders by filtering out the Parkinson's and Alzheimers conditions, keeping 'Health', 'Bipolar Disorder, Depression, Schizophrenia', 'Bipolar Disorder, Depression, Epilepsy, Schizophrenia', 'Bipolar Disorder', and 'Epilepsy', 'Depression', 'Schizophrenia'. This dataframe, similar to the first one, contained blank entries for Sex, BMI, and/or Age for some disorders, so I dropped all the columns except the bacterial genuses. Now, the dataframe looks the same as it did for the first model, but containing only the conditions listed above. 

Next, I wanted to try to model the disorders that contain the relevant information such as Age, BMI, and Sex to see if there was an improvement in the accuracy. I filtered the original dataframe to drop any rows that have zero entries for these columns. The remaining conditions are 'Health', 'Bipolar Disorder, Depression, Schizophrenia', 'Bipolar Disorder, Depression, Epilepsy, Schizophrenia', 'Bipolar Disorder', and 'Epilepsy'. Additional filtering had to be performed to remove any Age's less than one. The final dataframe for this model looks like this: 

![Orig](/assets/images/dt_neurowsex.jpg)  

Before modeling a decision tree, all the dataframes needed to be split into training and testing sets. This is necessary for the same reasons listed in the Naive Bayes tab. 

## Models 

1. DT with all data
   ![Orig](/assets/images/dt_alldata_plot.jpg)
   ![Orig](/assets/images/dt_alldata_graphs.jpg)  
3. DT - neurodegenerative disorders
   ![Orig](/assets/images/dt_neuro_plot.jpg)
   ![Orig](/assets/images/dt_neuro_graphs.jpg) 
5. DT - psychological disorders
   ![Orig](/assets/images/dt_psych_plot.jpg)
   ![Orig](/assets/images/dt_psych_graphs.jpg) 
7. DT with relevant attributes such as 'Age', 'BMI', 'Sex'
   ![Orig](/assets/images/dt_psych_sex.jpg)
   ![Orig](/assets/images/dt_psych_sex_graphs.jpg) 

### Model Accuracies 

| Model                                    | Accuracy |
| ---------------------------------------- | -------- | 
| All data                                 | 0.8882   |
| Neurodegenerative                        | 0.9841   |
| Psychological                            | 0.8754   |
| Psychological with Additional Attributes | 0.9333   | 


## Conclusions 

The decision trees performed very well on the different datasets. I think it's interesting the note the increase in accuracy between the psychological disorder data, and the psychological disorder data filtered to keep Age, BMI, and Sex. Even though some of the classes were lost in this filtering process, it points to the influence these factors have on the gut microbiome and corresponding neurological disorders. 





