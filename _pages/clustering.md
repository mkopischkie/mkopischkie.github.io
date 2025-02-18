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



## Data Prep

For clustering, I used the dataset named combined_data_with_extra_data.csv. This dataset contains all the cleaned data frome the GMRepo and the NCBI. Reading in the file, the original dataframe looked like this:

![Orig](/assets/images/orig_df_clust.jpg) 

Clustering only works on unlabaled, quantitative data, because it calculates distance measures, so I dropped the 'Country' and 'Sex' columns immediately. Although I would like to have kept the 'Age' and 'BMI' columns, the NCBI database was not consistent in reporting those measures, so I dropped those columns as well. Then, I printed out the unique neurological disorder values, and since an individual could have multiple, they are: 'Health', 'Parkinsons', 'Alzheimers', 'Bipolar Disorder, Depression, Schizophrenia', 'Bipolar Disorder, Depression, Epilepsy, Schizophrenia', 'Bipolar Disorder', 'Epilepsy', 'Depression', and 'Schizophrenia'. I created a dictionary to replace these disorders with integers instead. I saved the 'Condition' column as the label and dropped it from my dataframe. Now, my dataframe is ready for clustering and looks like this: 

![Final](/assets/images/final_df_clus.jpg) 

I am performing K-Means, Agglomerative Hierarchial Clustering, and DBSCAN on two different datasets. Where one was standardized, using StandardScalar() and the other was not. In the dataframe above, the values are all relative abundances of bacteria found in various microbiomes. Because these values are already scaled across the rows, standardizing may skew the data. On both datasets, PCA was performed to reduce the features to three for easy visualization. The amount of variance retained in the standardized datast is 16%, whereas the variance retained in the other dataset is 59%. The three features contributing the most to the first three components in each dataset are:

Standardized Dataset | Original dataset
-------------------- | ----------------
![Orig](/assets/images/stand_feat.jpg) | ![Orig](/assets/images/orig_feat.jpg) 

## Silhouette Method

 With StandardScalar() | Without StandardScalar() 
 --------------------- | -----------------------
![Orig](/assets/images/sil_standardscalar.jpg) | ![Orig](/assets/images/sil_without_standardscalar.jpg) 
![Orig](/assets/images/k=2_dend_ss.jpg) | ![Orig](/assets/images/k=3_dend_noss.jpg) 
 **k=2: K-Means**      | **k=3: K-Means**
![Orig](/assets/images/k=2_ss.jpg) | ![Orig](/assets/images/k=3_noss.jpg) 
![Orig](/assets/images/k=2_cent_ss.jpg) | ![Orig](/assets/images/k=3_cent_noss.jpg) 
Silhouette Score (K-means): 0.3314845735616456                |   Silhouette Score (K-means): 0.3627119322222995
Adjusted Rand Index (K-means):  -0.012740774016489093         | Adjusted Rand Index (K-means):  0.03621184786387432
Normalized Mutual Information (K-means):  0.0784546418604076  | Normalized Mutual Information (K-means):  0.07139054378464378   
**k=2: Hierarchial**   | **k=3: Hierarchial**
![Orig](/assets/images/k=2_hier_ss.jpg) | ![Orig](/assets/images/k=3_hier_noss.jpg) 
Silhouette Score (Hier.):  0.6742684861844029 | Silhouette Score (Hier.):  0.46529239268857936
Adjusted Rand Index (Hier.):  0.1311652836574616 | Adjusted Rand Index (Hier.):  0.014985469675248376
Normalized Mutual Information (Hier.):  0.22714965343103494 | Normalized Mutual Information (Hier.):  0.057293719384593496
**k=4: K-Means** | **k=6 K-Means**
![Orig](/assets/images/k=4_ss.jpg) | ![Orig](/assets/images/k=6_noss.jpg) 
![Orig](/assets/images/k=4_cent_ss.jpg) | ![Orig](/assets/images/k=6_cent_noss.jpg) 
Silhouette Score (K-means): 0.4493408014172253 | Silhouette Score (K-means): 0.42554559679547044
Adjusted Rand Index (K-means):  0.0710663060272605 | Adjusted Rand Index (K-means):  0.0020391650493911937
Normalized Mutual Information (K-means):  0.18472406309317152 | Normalized Mutual Information (K-means):  0.08978957460503154 
**k=4: Hierarchial** | **k=6: Hierarchial**
![Orig](/assets/images/k=4_hier_ss.jpg) | ![Orig](/assets/images/k=6_hier_noss.jpg) 
Silhouette Score (Hier.):  0.41848687396548534 | Silhouette Score (Hier.):  0.37813179739433733
Adjusted Rand Index (Hier.):  0.06980111084168736 | Adjusted Rand Index (Hier.):  -0.00996245154944142
Normalized Mutual Information (Hier.):  0.19600448151034447 | Normalized Mutual Information (Hier.):  0.09190474579544772
**k=9: K-Means** | **k=9: K-Means**
![Orig](/assets/images/k=9_ss.jpg) | ![Orig](/assets/images/k=9_noss.jpg) 
![Orig](/assets/images/k=9_cent_ss.jpg) | ![Orig](/assets/images/k=9_cent_noss.jpg) 
Silhouette Score (K-means): 0.3231579075476404 | Silhouette Score (K-means): 0.3844519181598884
Adjusted Rand Index (K-means):  0.06506612669825466 | Adjusted Rand Index (K-means):  0.011325299842002822
Normalized Mutual Information (K-means):  0.2004261662714766 | Normalized Mutual Information (K-means):  0.10566180768717398
**k=9: Hierarchial** | **k=9: Hierarchial**
![Orig](/assets/images/k=9_hier_ss.jpg) | ![Orig](/assets/images/k=9_hier_noss.jpg) 
Silhouette Score (Hier.):  0.29418343454100243 | Silhouette Score (Hier.):  0.30986398611475724 
Adjusted Rand Index (Hier.):  0.06192354838498244 | Adjusted Rand Index (Hier.):  0.0017529802511610218 
Normalized Mutual Information (Hier.):  0.20469003989447723 | Normalized Mutual Information (Hier.):  0.09271256576395098
**DBSCAN** | **DBSCAN**
![Orig](/assets/images/dbscan_ss.jpg) | ![Orig](/assets/images/dbscan_noss.jpg) 


## Additional Visualizations

<table>
  <tr>
    <td><img src="/assets/images/park_alz_health_clust.jpg" alt="Orig" width="600"></td>
    <td>
      <strong>Percent variance remaining after PCA:</strong> 99.9% <br>
      <strong>Most important features in first three PC's:</strong> Age, BMI, Sex_Male <br>
      <strong>Silhouette Score:</strong> 0.6686235956003335 <br>
      <strong>Adjusted Rand Index:</strong> 0.4723387314457915 <br>
      <strong>Normalized Mutual Information:</strong> 0.6504110441996591
    </td>
  </tr>
</table>








