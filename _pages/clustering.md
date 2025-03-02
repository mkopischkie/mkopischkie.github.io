---
title: "Clustering"
permalink: /clustering/
layout: single
classes: wide
---

## Methods 

**K-Means** works by randomly placing centroids and adjusting the position of the centroids until the average distance of the points inside the cluster from the centroids is minimized. Some of the distance metrics include Euclidean, Manhattan, and Cosine Similarity. The user specifies the number of clusters and an equal number of centroids are randomly selected from the data by the computer. The data points that are the closest to a centroid make up that cluster. The algorithm, from scikit-learn, calculates the average position of the points in the cluster and updates the coordinates of the centroid. Then, the distances between the new centroid and all the data points are calculated, the data points are reassigned to the closest cluster, and the centroid coordinates are updated. This process continues repeating until the centroids and clusters stop updating. 

![kmeans](/assets/images/kmeans_alg.jpg) 

**DBSCAN** clusters data points that are packed together, or have a high density, and labels the spread out points, or low density points, as outliers. This method relies on the parameter, eps, which defines the radius of the neighborhood around a data point. If there are a sufficient amount of neighboring datapoints within the given radius, the points are considered a cluster. If a point has at least min_samples neighbors within this radius, it is classified as a core point. Points within the radius of a core point but without enough neighbors to be core points themselves are classified as border points, while all other points are labeled as noise points. The algorithm iteratively selects points from the dataset and determines whether it is a core points or not. Then, the core points whose eps radius overlaps are considered to fall into the same cluster. This process continues repeating until all the points are identified as a member in a cluster or a noise point. 

![dbscan](/assets/images/dbscan_alg.jpg) 

There are two types of **Hierarchial Clustering**:
1. *Agglomerative* clustering uses a bottom-up approach where initially, each datapoint is treated as its own cluster. This method groups clusters together based on a distance metric. The algorithm identifies the clusters that are the closest together based on a specified distance metric, and merges the two clusters together. Then, the distance between the newly formed clusters and remaining clusters is recalculated based on the chosen linkage. This process continues until all the clusters are merged together, or a predefined number of clusters is met, and is easily represented by a dendrogram. 
2. *Divisive* clustering is a top-down approach where the data starts groupped together in one cluster. The algorithm recursively splits the cluster until a predefined number of clusters is met. The algorithm finds the best way to split a cluster into two subclusters, often using distance-based measures or techniques like k-means. This continues until the predefined stopped criteria is met.

![divisive](/assets/images/divisive.jpg) 

This image below clarifies the possible distance metrics used in clustering algorithms: 

![distance](/assets/images/distancemetrics.jpg) 


### Compare and Contrast Methods: 

![clustering](/assets/images/clustering.jpg) 

## Data Prep

My goal for clustering is to separate and classify neurological disorders based on their clusters. Although I will have to use PCA to visualize the clusters, because I have more than three features, I hope to observe distinguished clusters due to differences in gut bacteria. For the algorithms, I used the dataset named combined_data_with_extra_data.csv. This dataset contains all the cleaned data frome the GMRepo and the NCBI. Reading in the file, the original dataframe looked like this:

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

<table>
  <tr>
    <td><img src="/assets/images/sch_bi_dep_clust.jpg" alt="Orig" width="700"></td>
    <td>
      <strong>Percent variance remaining after PCA:</strong> 50% <br>
      <strong>Most important features in first three PC's:</strong> Bacteroids and Prevotella (2) <br>
      <strong>Silhouette Score:</strong> 0.5807762886916383 <br>
      <strong>Adjusted Rand Index:</strong> 0.13611382100414407 <br>
      <strong>Normalized Mutual Information:</strong> 0.2631590762011263
    </td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/assets/images/park_health_clust.jpg" alt="Orig" width="700"></td>
    <td>
      <strong>Percent variance remaining after PCA:</strong> 99.9% <br>
      <strong>Most important features in first three PC's:</strong> Age, Sex_Female, and Bacteroids <br>
      <strong>Silhouette Score:</strong> 0.7395707381103256 <br>
      <strong>Adjusted Rand Index:</strong> 0.1682006284167953 <br>
      <strong>Normalized Mutual Information:</strong> 0.31207464042723443
    </td>
  </tr>
</table>

<table>
  <tr>
    <td><img src="/assets/images/sch_health_clust.jpg" alt="Orig" width="700"></td>
    <td>
      <strong>Percent variance remaining after PCA:</strong> 91.5% <br>
      <strong>Most important features in first three PC's:</strong> Sex_Male, Bacteroids, and Faecalibacterium <br>
      <strong>Silhouette Score:</strong> 0.783469169325889 <br>
      <strong>Adjusted Rand Index:</strong> 0.05906551856661338 <br>
      <strong>Normalized Mutual Information:</strong> 0.22700065792920487
    </td>
  </tr>
</table>

## Conclusions

Standardizing my data with standard scalar produced a silhouette graph that indicates I should use k=2 and k=4. I also used k=9 because I have nine unique neurological disorders, some that are a combination of two. The dendrogram appears to recommend using a k=4. Without standardizing my data, the silhouette graph indicates that I should use k=3 and k=6. I also performed clustering with nine clusters for the reason I decsribed previously. Although unstandardized clusters have lower silhouette scores overall, the k values make more intuitive sense. The neurological disorders in my dataframe represent both neurodegenerative and psychiatric disorders, and a healthy control, representing the k=3. The k=9 I found most interesting between the standardized and unstandardized datasets. Even though the unstandarized clusters have a higher silhouette score, the standardized dataset has a higher NMI score, which represents how well the clustered labels fit the true labels. 

The DBSCAN clustering method has a hard time clustering more than two groups together. This makes sense given that all my data appears densely packed together and I'm analyzing small differences in bacteria or concentrations in the gut microbiome. However, DBSCAN still prints an interesting result for the standardized dataset. It appears to have two unique clusters, which could possibly represent the healthy control groups and those with neurological disorders. 

This led me to perform additional clustering on smaller datasets. I wanted to see if there was a difference in performance between neurdegenerative disorders with a healthy control, and between psychiatric diseases. Clustering between Parkinsons, Alzheimers, and a healthy control yielded very positive results. After completing PCA, 99.9% of the variance in my dataset was captured with the main contribution factors being age, bmi, and sex. I wanted to keep sex in this dataframe for clustering to see if it had an impact on the gut microbiome composition and neurological disorders. I used the command pd.get_dummies() and found that my scores were much higher than if I dropped sex from this dataframe. Aside from a high silhouette score, my NMI score is also quite high, indicating that the predicted labels line up with the true labels well. 

Although clustering with Schizophrenia, Bipolar Disorder, and Depression didn't yield has high of scores as the neurdegenerative disorders, there were still a couple of interesting insights. There was less variance was captured in the 3D visualization than for the neurodegenerative disorders. And the three most important features were Bacteroids and Prevotella, which appears twice. Going back to my visualizations with additional data, I see that Bacteroids are essentially missing from the psychiatric disorder microbiome, with a high increase in Prevotella in Bipolar Disorder as compared to the healthy control group. Indicating that the clustering results correlate well with what we would expect. 

Next, I wanted to see how individual neurological disorders would cluster against the healthy control group. First, Parkinsons maintained a high variance captured and silhouette score, but the NMI score was surprisingly low. I was curious if either the Parkinsons group or the Healthy group contributed more to the lower NMI score, so I ran a similar test with Schizophrenia and a Healthy control. I saw the same things with a high silhouette score but a low NMI score. I ran a confusion matrix and found that the algorithm was labeling more healthy individuals as individuals with schizophrenia. From this information, I believe that I need to collect more data, especially on a healthy control. 

Clustering between the healthy control and an individual neurological disorder separated very well. This would be useful in classifying a new sample. A larger model could be built on this that clusters each neurological disorder separately with the control group. Doing that separately may increase the overall accuracy, represented by the NMI score. 

Overall, both K-Means and Hierarchial Clustering separated the data well and generally performed better on smaller datasets. My next steps include: collecting more data, refining the algorithms, trying new clustering algorithms, and running confusion matricies if the NMI score is still low. 









