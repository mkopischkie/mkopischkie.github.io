---
title: "NN: Results"
permalink: /nn_results/
layout: single
classes: wide
---

Overall, the model results were fairly poor, but with continued hyperparamter tuning and incorporating more data could significantly improve results. The LSTM gave only a 20% accuracy with a loss of 2.5. The confusion matrix also showed poor results and showed that the model was not learning very well. 

cm image
graph image

This can be due to several reasons including: 

- Lack of training data. The model was trained on 800 data entries and tested on the remaining 200.
- Too many labels. After removing and combining certain labels, there were still 14 possible labels with some having significant overlap. For example, one label was 'Toxic if inhaled or swallowed' and the other was 'Fatal if inhaled or swallowed'. Chemical compounds are fickle and a change of only one or two atoms and/or how they are bonded can have extreme consequences. To mitigate this problem, there would need to be more training data or logical rules involved in the model so that it's not relying entirely on a traditional neural network.
- Not having an even amount of entries for each label. Even though I significantly reduced the labels, some were seen more often than others. Some labels appeared over 200 times and others less than 100. Even though this isn't a significant difference, it could still contribute to the poor performance.
- Overfitting. Even though I included a dropout layer to prevent overfitting, the validation accuracy is still lower than the training accuracy. This indicates that the model is familiar and performing best on data it has seen, but not all the rules can be applied generaically.



