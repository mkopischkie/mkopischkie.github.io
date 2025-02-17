---
title: "Principal Component Analysis"
permalink: /pca/
layout: single
classes: wide
---

Reducing the dimensionality of datasets is imperative to utilizing data science and machine learning techniques. It reduces the time and computational complexity while maintaining a certain percentage of the variance. Principal Component Analysis (PCA) is a dimensionality reduction technique that can be utilized by data scientists’ and others in a multitude of fields including machine learning, finance, and healthcare. Essentially, the data is transformed into a new coordinate system where the features that contribute most to the variance in the dataset can be easily identified [1]. The four main calculations involved in PCA include: calculating the covariance matrix, the eigenvalues, and the corresponding eigenvectors.

Where the covariance matrix is "a measure of how changes in one variable are associated with changes in a second variable. Specifically, it’s a measure of the degree to which two variables are linearly associated.” [2]. From the covariance matrix, the eigenvalues are calculated by subtracting the identitiy matrix by the unknown eigenvalue, subtracting the product from the covariance matrix, and setting the difference equal to zero. The eigenvalues quantify how much a linear transformation is stretched or shrunk. The corresponding eigenvectors are calculated by multiplying the difference between the covariance matrix and the product of the eigenvalue and the identity matrix, by an n-dimensional vector and setting the product equal to zero. An eigenvector represents a direction of the linear transformation. The principal components correspond to the largest eigenvalues. Therefore, our first principal component will have the greatest variance and the largest eigenvalue. The second principal component will have the second largest variance and the second largest eigenvalue, and so on. For more information on the mathematical concepts behind PCA, please see my paper attached to the homepage on this website. On this tab, I will demonstrate performing PCA in Python. 

On the previous visualization page, I filtered out the least popular bacteria for each neurological disorder. I will be using the dataframe obtained from the threshold to use PCA because when I tried to use the full panel dataframes, the numbers and visualizations were extremely difficult to interpret. I created a .csv file called combined_data_with_extra_data that contains clean data from the GMRepo and NCBI. I will be performing PCA on the Parkinsons and Healthy neurological disorders, so I filter my large dataframe to obtain the two phenotypes. I drop any non-numeric column except sex, which I use the pd.get_dummies() command to transform the categories into integers. Since determining whether sex is a driving factor in the gut microbiome and neurological disorders, I want to keep the variable to see how it affects the data. Then I create my target variable by isolating the 'Condition' column, using a dictionary to replace the values, 'Health' and 'Parkinsons' with 0 and 1 respectively, saving the label, and dropping the column. So, now my dataframe looks like this:

![Original](/assets/images/park_pca_df_orig.jpg) 


Now that all my features are numeric attributes, I can begin the PCA computation. Arguably, the most important part of PCA is standardization. This method is sensitive to the scale of different attributes and it could disproportionately represent the variance of a certain attribute, so I standardize my data using StandardScalar().  


Next, I specify that I want to see the first three principal components and print the explained variance ratio. This tells us the first three principal components, and how much variance they contribute to the dataset. My output indicates that the first PC is responsible for 0.15852208 of the variance, the second PC is respondible for 0.1002905 of the variance, and the third is responsible for 0.09367044. These first three components only represent about 3.5% of the variance in my dataset. However, this makes sense given that this data frame is trimmed from the full panel and each column has a heavier weight. 

The following graph represents the first three principal components: 

![Label](/assets/images/pca3_park.jpg) 

The graph has a noticeable divide between the Parkinsons neurological disorder and the healthy control. The three features contributing the most to the first three principal components are: 

![Important](/assets/images/park_most_impor.jpg) 

Plotting the PCA in 2D still contained the visible divide between Parkinsons and the healthy control 

![pca2](/assets/images/pca2_park.jpg) 

Moving on from the top principal components, I measured the cummulative variance of all the principal components and plotted it to visually interpret the information 

![cumvar](/assets/images/cumvar_park.jpg) 

Then, I created a new data frame that retains at least 95% of the variance from the original data frame. 

![95df](/assets/images/park_pca_df_end.jpg) 

This new dataframe only removed three principal components, which I expected since I did the computation using the dataframe obtained with the threshold. 



### References
[1] GeeksforGeeks. Mathematical approach to pca. https://www.geeksforgeeks.org/mathematical- approach-to-pca/, n.d. Accessed: 2024-12-06.

[2] Statology. How to read a covariance matrix. https://www.statology.org/how-to-read-covariance- matrix/, n.d. Accessed: 2024-12-06.

