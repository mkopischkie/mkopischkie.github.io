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
