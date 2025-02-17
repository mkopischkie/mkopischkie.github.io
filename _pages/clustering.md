---
title: "Clustering"
permalink: /clustering/
layout: single
classes: wide
---

## Methods 

K-Means works by randomly placing centroids and adjusting the position of the centroids until the average distance of the points inside the cluster from the centroids is minimized. The user specifies the number of clusters and an equal number of centroids are randomly selected from the data by the computer. The data points that are the closest to a centroid make up that cluster. The algorithm, from scikit-learn, calculates the average position of the points in the cluster and updates the coordinates of the centroid. Then, the distances between the new centroid and all the data points are calculated, the data points are reassigned to the closest cluster, and the centroid coordinates are updated. This process continues repeating until the centroids and clusters stop updating. 

DBSCAN clusters data points that are packed together, or have a high density, and labels the spread out points, or low density points, as outliers. This method relies on the parameter, eps, which defines the radius of the neighborhood around a data point. 

## K-Means 



## DBSCAN



## Hierarchial 
