---
title: "Principal Component Analysis"
permalink: /pca/
layout: single
classes: wide
---

Reducing the dimensionality of datasets is imperative to utilizing data science and machine learning techniques. It reduces the time and computational complexity while maintaining a certain percentage of the variance. Principal Component Analysis (PCA) is a dimensionality reduction technique that can be utilized by data scientists’ and others in a multitude of fields including machine learning, finance, and healthcare. Essentially, the data is transformed into a new coordinate system where the features that contribute most to the variance in the dataset can be easily identified [1]. The four main calculations involved in PCA include: calculating the covariance matrix, the eigenvalues, and the corresponding eigenvectors.

Where the covariance matrix is "a measure of how changes in one variable are associated with changes in a second variable. Specifically, it’s a measure of the degree to which two variables are linearly associated.” [2]. From the covariance matrix, the eigenvalues are calculated by subtracting the identitiy matrix by the unknown eigenvalue, subtracting the product from the covariance matrix, and setting the difference equal to zero. The eigenvalues quantify how much a linear transformation is stretched or shrunk. The corresponding eigenvectors are calculated by multiplying the difference between the covariance matrix and the product of the eigenvalue and the identity matrix, by an n-dimensional vector and setting the product equal to zero. An eigenvector represents a direction of the linear transformation. The principal components correspond to the largest eigenvalues. Therefore, our first principal component will have the greatest variance and the largest eigenvalue. The second principal component will have the second largest variance and the second largest eigenvalue, and so on. 

For more information on the mathematical concepts behind PCA, please see my paper attached to the homepage on this website. On this tab, I will demonstrate performing PCA in Python on my full panel schizophrenia data frame. 

On the previous visualization page, I filtered out the schizophrenia dataset so that only the most common bacteria found were apart of it. But to perform PCA, I want the full panel of the gut microbiota for each sample, so I commented out the threshold requirement, converted the Mesh ID's to the specific conditions, and saved it as a new data frame 

*insert image 

Now, I have the full panel data frames for schizophrenia males and females, and healthy males and females. To create a target variable, I concatanated these data frames together and changed the 'Condition' column to 1 and 0, indicating schizophrenia or not, respectively. 

*insert image

I saved the label and dropped it from the data frame, as PCA requires only quantitative data. Additionally, I dropped the 'Run ID' column and the 'Country' column. Encoding would not have worked correctly using PCA, because even though the countries could have been turned to numbers, the column is still categorical, which would have swayed my computation. However, I one-hot-encoded the gender column because I want to know if gender impacts the gut microbiome for schizophrenic patients. 

*insert image 

Now that all my features are numeric attributes, I can begin the PCA computation. Arguably, the most important part of PCA is standardization. This method is sensitive to the scale of different attributes and it could disproportionately represent the variance of a certain attribute, if not standardized. 

*insert image

Next, I specify that I want to see the first three principal components and print the explained variance ratio. This tells us the first three principal components, and how much variance they contribute to the dataset. 

*insert image 

These first three components only represent about 6% of the variance in my dataset. However, this makes sense given that this data frame contains 513 rows and 1152 columns. Therefore, the maximum amount of principal components can be 513. So, the larger number of components indicates that we may see a smaller variance contribution from just the first three principal components. I used the following code to print a graph in three dimensions and obtained the following result.

*inesrt image

*insert image 

The graph is difficult to interpret because these three components only account for 6% of the variance in the dataset. The following two blocks of code extract the first three principal components and the features that contribute the most to each component. 

*insert image

The same process is completed for the 2-component PCA and I found that the first two components only contain 5% of the variance in the dataset. Using the same code from above, I plotted the two dimensional PCA. 

*insert image

Moving on from the top principal components, I measured the cummulative variance of all the principal components. 

*insert image 

I plotted the cummulative variance to visually interpret the information. 

*insert image

Then, I created a new data frame that retains at least 95% of the variance from the original data frame. 

*insert image

Even though this new dataframe still has 300 dimensions, PCA reduced over 200 dimensions from the given dataframe. In the following code, we're able to see the eigenvectors and the eigenvalues of the covariance matrix. 

*insert image 

The same process was done for Alzheimer's, Parkinson's, Epilepsy, Bipolar Disorder, and Depression. PCA was successful in reducing the dimensions in all of the mentioned dataframes. 



### References
[1] GeeksforGeeks. Mathematical approach to pca. https://www.geeksforgeeks.org/mathematical- approach-to-pca/, n.d. Accessed: 2024-12-06.

[2] Statology. How to read a covariance matrix. https://www.statology.org/how-to-read-covariance- matrix/, n.d. Accessed: 2024-12-06.

