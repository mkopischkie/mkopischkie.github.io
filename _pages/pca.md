---
title: "Principal Component Analysis"
permalink: /pca/
layout: single
classes: wide
---

Reducing the dimensionality of datasets is imperative to utilizing data science and machine learning techniques. It reduces the time and computational complexity while maintaining a certain percentage of the variance. Principal Component Analysis (PCA) is a dimensionality reduction technique that can be utilized by data scientists’ and others in a multitude of fields including machine learning, finance, and healthcare. Essentially, the data is transformed into a new coordinate system where the features that contribute most to the variance in the dataset can be easily identified. The four main calculations involved in PCA include: calculating the covariance matrix, the eigenvalues, and the corresponding eigenvectors.

Where the covariance matrix is "a measure of how changes in one variable are associated with changes in a second variable. Specifically, it’s a measure of the degree to which two variables are linearly associated.” [2]. From the covariance matrix, the eigenvalues are calculated by subtracting the identitiy matrix by the unknown eigenvalue, subtracting the product from the covariance matrix, and setting the difference equal to zero. The eigenvalues quantify how much a linear transformation is stretched or shrunk. The corresponding eigenvectors are calculated by multiplying the difference between the covariance matrix and the product of the eigenvalue and the identity matrix, by an n-dimensional vector and setting the product equal to zero. An eigenvector represents a direction of the linear transformation. The principal components correspond to the largest eigenvalues. Therefore, our first principal component will have the greatest variance and the largest eigenvalue. The second principal component will have the second largest variance and the second largest eigenvalue, and so on. 

For more information on the mathematical concepts behind PCA, please see my paper attached to the homepage on this website. On this tab, I will demonstrate performing PCA in Python on my full panel schizophrenia data frame. 
