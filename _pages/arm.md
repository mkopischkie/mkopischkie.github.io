---
title: "Association Rule Mining"
permalink: /arm/
layout: single
classes: wide
---

## Overview 

Association Rule Mining (ARM) is an unsupervised machine learning technique that finds highly associated items in a transaction. Three ways to measure the association are with support, confidence, and lift. 
- Support is calculated by the divison of the number of times a specific itemset appears, by the total amount of transactions in the dataset. It measures how frequently an itemset appears in the dataset
- Confidence is calculated by summing the transactions containing both items and dividing by the number of transactions containing the first item. It measures how frequently two or more itemsets appear together, relative to how often the first itemset appears.
- Lift is calculated by dividing the confidence of a rule by the support. In other words, it measures how much more likely an item it to occur if the consequent item occurs with it.

![measurements](/assets/images/arm_measurements.jpg) 

The rules themselves are if-then statements that describe the probability of relationships in data. For instance, there is a probability of a relationship between people who exercise everyday and those who don't suffer from cardiovascular problems. We can measure these associations with the measurements I described above. ARM is frequently used in market-basket analysis, where if a social media consumer watches a video, it will recommend others similar to it based consumer behavior that is quantifable with support, confidence, and/or lift. 

Implementation of association rule mining into Python or R is easy with the use of the Apriori algorithm. Initially, the algorithm combs through the data and labels an item as frequent or not from a threshold set by the user. If the user sets the threshold at 0.40, then the algorithm will only return frequent 1-itemsets if it occurs in 40% of all the transactions. Any item that does not meet this threshold will not be considered for higher frequent itemsets. Those that do, the algorithm will generate a 2-itemset and check whether the 2-itemset reaches the threshold. This gets computationally expensive pretty quickly as the algorithm has to scan the data multiple times to generate the frequent itemsets. The length of these itemsets is dictated by the user, as a max_len parameter can be specified in the apriori() command. 

In the scope of my project, I am conducting the Apriori method two different ways. One on the whole dataset and another on parts of the dataset that were divided based on neurological disorders. The goal is to determine the more frequent itemsets between a neurological disorder and bacteria. Ideally, I can generate and visualize the frequent patterns between particular disorders and the corresponding bacteria in the gut microbiome. 

## Data Prep

Association rule mining and the Apriori algorithm requires data in a transaction format. This can look several different ways. To perform apriori in Python, I will use my combined_data csv file pictured below. 

![Orig](/assets/images/combined_df.jpg) 

My goal is to replace the relative abundances with the column names they occur in. First, I drop any numerical data, such as Age, BMI, and Country, that would not make sense if it was replaced with the column name. Then, I can replace the non-zero relative abundances with the column name. I drop the column names and replace them with numbers corresponding to the column, as transaction data does not have any column names. To make the data look like transaction data, I put the data into a list, put the non-zero entries first, and put the list back into a dataframe. The new transaction data is kept in the col_names_trans_data.csv file and is pictured below. 

![Final](/assets/images/trans_data.jpg) 

For more specific association rules, I binned the relative abundances from the combined_df file to have each relative abundance be filled with a low, medium, or high bacterial genus. I used the same process above so that the binned transaction data is named col_names_disc_trans_data.csv and pictured below. 

image

I used the apriori algorithm a couple different ways, one where I separated the transaction data into neurological disorders, one where I used the algorithm on the whole dataset, and another where I used the algorithm on the whole discretized dataset. I will walk through the algorithm that I used to generate association rules on the Parkinsons transaction data specifically. 

In the ARM Parkinsons notebook, I separated the transactions with Parkinsons and isolated the items. With these isolated, I performed one-hot-encoding so that the bacterial names would again be the column names with a binary 0 or 1 indicating the presense or lack thereof in each transaction. 

image

Then, I used the apriori algorithm to generate the frequent itemsets. For the Parkinsons transactions, I used a high min_support threshold because the majority of the bacterial names reoccur in each row. 












