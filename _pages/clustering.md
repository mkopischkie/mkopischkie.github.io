---
title: "Clustering"
permalink: /clustering/
layout: single
classes: wide
---

## Methods 

**K-Means** works by randomly placing centroids and adjusting the position of the centroids until the average distance of the points inside the cluster from the centroids is minimized. The user specifies the number of clusters and an equal number of centroids are randomly selected from the data by the computer. The data points that are the closest to a centroid make up that cluster. The algorithm, from scikit-learn, calculates the average position of the points in the cluster and updates the coordinates of the centroid. Then, the distances between the new centroid and all the data points are calculated, the data points are reassigned to the closest cluster, and the centroid coordinates are updated. This process continues repeating until the centroids and clusters stop updating. 

**DBSCAN** clusters data points that are packed together, or have a high density, and labels the spread out points, or low density points, as outliers. This method relies on the parameter, eps, which defines the radius of the neighborhood around a data point. If there are a sufficient amount of neighboring datapoints within the given radius, the points are considered a cluster. If a point has at least min_samples neighbors within this radius, it is classified as a core point. Points within the radius of a core point but without enough neighbors to be core points themselves are classified as border points, while all other points are labeled as noise points. The algorithm iteratively selects points from the dataset and determines whether it is a core points or not. Then, the core points whose eps radius overlaps are considered to fall into the same cluster. This process continues repeating until all the points are identified as a member in a cluster or a noise point. 

There are two types of **Hierarchial Clustering**:
1. *Agglomerative* clustering uses a bottom-up approach where initially, each datapoint is treated as its own cluster. This method groups clusters together based on a distance metric. The algorithm identifies the clusters that are the closest together based on a specified distance metric, and merges the two clusters together. Then, the distance between the newly formed clusters and remaining clusters is recalculated based on the chosen linkage. This process continues until all the clusters are merged together, or a predefined number of clusters is met, and is easily represented by a dendrogram. 
2. *Divisive* clustering is a top-down approach where the data starts groupped together in one cluster. The algorithm recursively splits the cluster until a predefined number of clusters is met. The algorithm finds the best way to split a cluster into two subclusters, often using distance-based measures or techniques like k-means. This continues until the predefined stopped criteria is met.


### Compare and Contrast Methods: 



## K-Means 



## DBSCAN



## Hierarchial 
