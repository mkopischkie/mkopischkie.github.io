---
title: "Decision Tree"
permalink: /dt/
layout: single
classes: wide
---

## Overview 

Decision trees are non-parametric supervised learning model. Non-parametric models do not assume any preexisting relationships in the data, so they can model complex and non-linear relationships. Decision trees are a top-down, greedy algorithm that splits the data into classes until a specified depth is reached. It's easy to think of decision trees as flow charts where each branch represents an answer to a question. 

image 

The way that a decision tree is split up is influenced by metrics such as Information Gain and Gini Impurity. Information gain measures how well a question will separate the data. For example, in the image above, one of the questions would be 'Is there a swell?' and the information gain is measured by the split in the answers. There would be a high information gain if, when there was a swell, everyone surfed, and if there isn't a swell, no one would surf. 

The information gain is highly correlated with entropy, which is the measure of randomness and disorder. For instance, if three people surfed when there was no swell and three people did not surf with no swell, the entropy would be high since there is more randomness to decide whether to surf or not. The increase in entropy correlates with a decrease in information gain, since there is not a clear answer to the question asked. 
