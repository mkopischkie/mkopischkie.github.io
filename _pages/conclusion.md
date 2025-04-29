---
title: "Conclusion"
permalink: /conclusion/
layout: single
classes: wide
---

The research I've provided implies that there is a strong relationship between the gut microbiome and neurological disorders. I mainly modeled neurodegenerative, psychological, and a combination of those disorders. The reason for these datasets is because I intent to create a model capable of distinguishing between multiple disorders, not just between a healthy control and a disorder. However, clustering and using PCA between a healthy control and a single neurological disorder indicated that the data would split very well. 

| Clustering | Boxplot | 
| ---------- | ------- |
| ![kmeans](/assets/images/park_health_clust.jpg) | ![kmeans](/assets/images/boxplots_sanitycheck.jpg) |

Further clustering implied that the rest of my data, including a combination of disorders, would split well. The 'Additional Visualizations' section under the clustering tab proved that modeling the neurodegenerative and psychological disorders separately may work the best. I assume that this is because the neurodegenerative dataframe is able to maintain more features, such as Age and Sex. Furthermore, there is more of an overlap between psychological disorders than disorders like Parkinsons or Alzheimers. For example, someone can have Bipolar Disorder and Depression, not just one or the other. 

Although all the supervised models performed very well with accuracies over 80%, the psychological disorders dataframe consistently had lower accuracies than the neurodegenerative dataframe. Again, this could be due to the overlap between psychological disorders and the lack of features available for modeling. Additionally, there were different ways for these overlaps to be modeled. Such as adding a duplicate row for each unique disorder or treating every combination of psychological disorders as a unique condition. Regardless, the accuracy increased in decision tree modeling when I dropped any row in the psychological disorder dataframe that had a zero value. This way, I maintained the features such as Sex, Age, and BMI. The increase in accuracy between these changes may be due to fewer classes and/or that Sex, Age, and BMI have an affect on an individuals' neurological state. 

It appears that the ensemble methods fit the dataframes best, which makes sense given that ensemble methods are based on models such as deicison trees and designed to increase the accuracy. But, there is a chance that these models are overfitting the data, indicated by the 100% accuracy provided by the random forest for the neurodegenerative data. To prove if this is the case, I would gather more data on the gut microbiome for a healthy control and people with Parkinsons or Alzheimers, retrain the model, and assess the accuracy. However, XGBoost yielded accuracies over 90% for the combined conditiona and the neurodegenerative disorders. This model appears to overfit the data less than the random forest, so with the data I currently have, XGBoost appears to fit the data the best. Specifically, it fits the combined neurological disorders well, which shows a lot of promise for this research project. 

XGBoost creates decision trees from samples of the dataset (without replacement) and learns and adjusts the weights for the next model based on the previous trees' mistakes. Because this method uses decision trees, the continuous data types I have work very well because there are an infinite ways to construct the trees. The XGBoost package in the sci-kit learn library has a feature importance plot which is very useful in this project. If I were to model a dataset that contains a healthy control and individuals with one neurological disorder, I could use XGBoost and the feature importance to determine the features that contribute the most to the prediction. This could be useful in diagnosis and drug development for neurological disorders. 

Overall, this project has strong findings and potential for further research. Some areas that need to be addressed still are handling the overlapping conditions and any instances of overfitting. I hope to continue this project into Deep Learning and comapre how neural nets perform against traditional supervised machine learning models. These findings so far are very promising and can have huge implications on the healthcare industry. Outside of this class, I plan on addressing the concerns listed above, improving the XGBoost model, and isolating the important features for diagnosing each neurological disorder. 



