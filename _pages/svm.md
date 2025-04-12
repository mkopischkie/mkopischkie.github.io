---
title: "Support Vector Machine"
permalink: /svm/
layout: single
classes: wide
---

<script type="text/javascript" async
  src="https://polyfill.io/v3/polyfill.min.js?features=es6">
</script>
<script type="text/javascript" async
  id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

## Overview 

A Support Vector Machine (SVM) is a supervised, non-parametric, and discriminitive, machine learning model. In other words, it learns from a training set of the data, does not assume any pre-existing relationships, and fits a data vector into a defined category. 

Initially, the algorithm computs the dot product between two vectors to gain insight into how similar the vectors are related. For example, if the dot product between two vectors is zero, the two vectors are perfectly orthogonal, and if the dot product is one, the vectors are perfectly parallel. The dot product is defined as 

$$x \cdot y = \left|\left|x\right|\right| \left|\left|y\right|\right| cos(\theta)$$

where 
$\theta$
is the angle measured between the two vectors. 

Generally, SVM's try to separate the data with a plane through space. In two or three dimensions, the data may be linearly separable, as depicted in the image below. But often, a linear boundary will not separate the data well, so a non-linear hyperplane is necessary. 

![Orig](/assets/images/svm1.jpg) 

In higher dimensions, rather than representing the hyperplane as a normal line equation, we rewrite it in terms of vector multiplication and addition. 

$$ w \cdot x + b = 0 $$

Where w is the weight vector, x is a vector of the predictors, and b is a scalar term representing the bias which shifts the decision boundary. Generally, the points are then classified based on whether they fall above or below the decision boundary. 

The algorithm can accept different kernels, or tools to identify unique patterns 
1. Linear: as the name implies, the linear kernel works best for data that can be linearly separated in higher-dimension space. The algorithm works in the same sized feature space as the data provided. It is quick and less prone to over fitting the high dimensional data.

$$ K(x^T, x') = x^T \cdot x' $$

2. Polynomial: the algorithm transforms the data into a higher dimensional space where the decision boundaries are curved. Therefore, it can capture nonlinear patterns in the data. It's best to use this kernel if there may be interactive features in the data. In other words, when the effect of one variable modifies another. The user determines the complexity of the algorithm, but a larger complexity increases the chance of overfitting.

$$ K(x^T, x') = (\gamma x^T \cdot x' + r)^d $$

4. RBF/Gaussian: the data is mapped to an infinite-dimension space where the decision boundaries are very flexible. This is the best general-purpose model for nonlinear and complex relationships in data. Instead of using the dot product, it uses the euclidean distance to measure the similarity between two points. The user can tune the parameters, but without caution, this can lead to overfitting.

$$ K(x, x') = exp(=\gamma \left|\left| x - x'\right|\right|^2) $$

To show an example of how we can cast a point into a higher dimension, I'll write out an example using the polynomial kernel with a constant of one and a two degree polynomial. 

$$
\begin{align*}
K(x, x') &= (\gamma x \cdot x' + r)^d \\
         &= (\gamma x \cdot x' + 1)^2 \\
         &= (x_1 x_1' + x_2 x_2' + 1)^2 \\
         &= x_1^2 {x_1'}^2 + x_2^2 {x_2'}^2 + 1 + 2 x_1 x_1' x_2 x_2' + 2 x_1 x_1' + 2 x_2 x_2'
\end{align*}
$$

Now, we can rewrite this equation into the feature map function with vector notation. Essentially, we want to write the above final equation in the form of 
$K(x, x') = \phi(x)^T \cdot \phi(x')$
and I will perform this computation below. 

$$
\begin{align*}
K(x, x') &= x_1^2 {x_1'}^2 + x_2^2 {x_2'}^2 + 1 + 2 x_1 x_1' x_2 x_2' + 2 x_1 x_1' + 2 x_2 x_2' \\
         &= \begin{pmatrix}
             x_1^2 \\
             x_2^2 \\
             \sqrt{2} x_1 x_2 \\
             \sqrt{2} x_1 \\
             \sqrt{2} x_2 \\
             1
         \end{pmatrix}^\top
         \begin{pmatrix}
             x_1'^2 \\
             x_2'^2 \\
             \sqrt{2} x_1' x_2' \\
             \sqrt{2} x_1' \\
             \sqrt{2} x_2' \\
             1
         \end{pmatrix}
\end{align*}
$$

Now we can see that this feature map will map a two-dimensional data points into six-dimensional space because there are six unique components in the feature-mapping vectors. 

Another important thing to note about SVM's, is the way the decision boundary is drawn. The space from the decision boundary to the nearest datapoint on either sides is called the margin. And an SVM can either have a hard or soft margin. A hard margin indicates better separation of the data where all the data points of one class fall on one side, and the data belonging to the other class, falls on the other side. A soft margin on the other hand, allows a couple of data points to be on the wrong side. A soft margin could indicate nonlinear, complex relationships, or influential outliers. A visual representation of the decision boundaries for the three kernels are pictured below. 

| Linear Kernel | Poly Kernel | RBF Kernel |
|---------------|-------------|------------|
|![Orig](/assets/images/decision_boundary_linear_svm.jpg)|![Orig](/assets/images/decision_boundary_poly_svm.jpg)|![Orig](/assets/images/decision_boundary_rbf_svm.jpg)|   

I will use SVM's on the final_df.csv file to try to create a hyperplane through my data to classify a point as having a particular neurological disorder or not. 


## Data Prep





## Model Evaluation 





## Conclusions
