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

Since SVMs work with complex math, the best data types are float and integer type numbers. For example, an SVM wouldn't perform as well with ordinal encoding, but it would perform better with one-hot-encoding. This has to do with the dot product computation, and interpreting a parallel or orthogonal dot product simplifies the classification more than a dot product of one and two that ordinal encoding may yield. 

In my final_df.csv dataframe, the only encoding necessary was in the Sex column, which only had male or female entries. I encoded male as 1 and female as 0, for the reasons stated above. Otherwise, depending on what I'm modeling, the features were already float numbers, representing the relative abundance of a bacterial genus. I chose to model all disorders, neurodegenerative disorders, and psychological disorders. The original dataframe is pictured below. 

![Orig](/assets/images/combined_df.jpg) 

To prepare the model containing all the neurological disorders, I dropped the Sex, Age, BMI, and Country columns because not every sample has entries for these attributes. I was left with the label and the relative abundances of the bacteria for each sample. I was also left with this same dataframe to model the psychological disorders, but the samples with diagnosed Parkinsons or Alzheimers were dropped. 

![Orig](/assets/images/dt_alldata.jpg) 

For modeling only the neurodegenerative disorders, I kept the Sex and Age column, but dropped BMI as many of the entries contained zero values. So, I was left with the label, Sex, Age, and the bacterial relative abundances for each sample. 

![Orig](/assets/images/dt_neuro.jpg) 


Each dataframe was split into an 80% training set and 20% testing set. Once again, the training and testing are mutually exclusive. In other words, no entry apart of the training set can also be included in the testing set. If this was not the case, the model would overfit and have an inflated accuracy from memorizing the data. In turn, it would not perform well on any new data that it has not yet seen. An example of the training and testing sets from the dataframe containing all the neurological disorders is pictured below. Please note that for the dataframes containing additional attributes such as Sex, Age, or BMI, the training and testing sets would reflect this. 

| X_train (data)                        | y_train (label)                       |
| ------------------------------------- | ------------------------------------- |
| ![Orig](/assets/images/x_train_dt.jpg) | ![Orig](/assets/images/y_train_dt.jpg) | 

| X_test (data)                        | y_test (label)                       |
| -------------------------------------| ------------------------------------ |
| ![Orig](/assets/images/x_test_dt.jpg) | ![Orig](/assets/images/y_test_dt.jpg) |

To find the optimal parameters where the SVM would perform the best on each dataset, I performed a GridSearchCV. The parameters that the model takes are the kernel and the C value. The C value is the regularization parameter that quantifies the balance between a low error and a large margin. A small C is a model that is more tolerant of misclassified data points, but maintains a large margin around the decision boundary. A large C prioritizes proper classification with high accuracy, rather than maintaining a large margin. Therefore, the area around the decision boundary is smaller. A model with a large C is more prone to overfitting and is not as generalizable. In my GridSearchCV, I performed cross-validation while fitting the data to a linear, poly, or rbf kernel, with possible regularization parameters as 0.1, 1, 10, or 100. Both dataframes composed of all the data and of only the psychological disorders performed best with an rbf kernel and a regularization parameter of 100. The neurological disorder dataframe, however, performed best with a linear kernel and a regularization parameter of 10. 

With my four dataframes and corresponding parameters, I was able to fit the model to the data and obtained the results below. 


## Model Evaluation 

1. SVM - all data (kernel = rbf, C=100)
   ![Orig](/assets/images/svm_alldata_graphs.jpg)
2. SVM - neurodegenerative (kernel = linear, C=10)
   ![Orig](/assets/images/svm_neuro_graphs.jpg)
3. SVM - psychological (kernel = rbf, C=100)
   ![Orig](/assets/images/svm_psych_graphs.jpg)

Accuracies: 

| Model                 | Accuracy |
|-----------------------|----------|
| All data              | 0.8789   |
| Neurodegenerative     | 0.9531   | 
| Psychological         | 0.8586   | 

### Experimental Models 

1. Neurodegenerative with RBF kernel, C=1

  | Confusion Matrix                                 | Classification Report | 
  |--------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_rbf_c1_graphs.jpg) | ![Orig](/assets/images/svm_rbf_c1_report.jpg)    | 

2. Neurodegenerative with RBF kernel, C=10

  | Confusion Matrix                                 | Classification Report | 
  |--------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_rbf_graphs.jpg) | ![Orig](/assets/images/svm_rbf_c10_report.jpg)   | 
   
3. Neurodegenerative with RBF kernel, C=100

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_rbf_c100_graphs.jpg) | ![Orig](/assets/images/svm_rbf_c100_report.jpg) | 

4. Neurodegenerative with Poly kernel, C=1

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_poly_c1_graphs.jpg) | ![Orig](/assets/images/svm_poly_c1_report.jpg)     | 
  
5. Neurodegenerative with Poly kernel, C=10

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_poly_graphs.jpg) | ![Orig](/assets/images/svm_poly_c10_report.jpg)  | 

6. Neurodegenerative with Poly kernel, C=100

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_poly_c100_graphs.jpg) | ![Orig](/assets/images/svm_poly_c100_report.jpg)     | 
  
7. Neurodegenerative with Linear kernel, C=1

  | Confusion Matrix                                | Classification Report | 
  |-------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_c1_graphs.jpg) | ![Orig](/assets/images/svm_linear_c1_report.jpg)   | 

8. Neurodegenerative with Linear kernel, C=10

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_linear_c10_graphs.jpg) | ![Orig](/assets/images/svm_linear_c10_report.jpg)   | 

9. Neurodegenerative with Linear kernel, C=100

  | Confusion Matrix                                  | Classification Report | 
  |---------------------------------------------------|-----------------------|
  | ![Orig](/assets/images/svm_neuro_c100_graphs.jpg) | ![Orig](/assets/images/svm_linear_c100_report.jpg)   | 

## Conclusions

Overall, the different SVMs fit the data quite well. The GridSearhCV parameters returned accuracies all over 85%, with the linear kernels performing the best. One thing I find interesting is that the neurodegenerative dataframe with a linear kernel with costs 10 and 100. The interesting thing here is that the confusion matricies are different. The kernel with a cost of 10 has one false negative and the kernel with a cost of 100 has three false positives. Given the scope of this project, the confusion matrix with the fewest false negatives is most likely the better model. A false negative means that someone who does have a neurological disorder, returns a negative test, indicating that they would not have the disorder. In a real scenario, false negatives mean that someone who needs treatment, is not getting it. 

In this case, to model the neurodegenerative disorders, a linear kernel with a cost of 100 is probably the best model, even though the GridSearchCV recommended otherwise. In the future, the best way to handle this may be with a cost matrix, where false negatives are more heavily penalized than false positives. Or, manually setting weights to avoid false negative predictions. 


