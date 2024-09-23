# Machine Learning Basics

## K-Nearest Neigbors (KNN)
<img src="https://media.geeksforgeeks.org/wp-content/uploads/20231207103856/KNN-Algorithm-(1).png" height="300">

- Given a set of labeled data points, when encountering an unlabeled test data point, we can accurately label it by finding its "nearest neighbor" in the points we already know.
- Consider top k nearest neighbors when labeling, majority vote.
- The top k nearest neighbors are determined by a chosen distance metric: Euclidean, Manhattan, Minknowski.
- Can also perform regression by averaging the target values obtained from top k nearest neighbors.

## Linear Regression
- Fits a linear model for dependent variable $y$ and potentially multiple independent variables $x_1, x_2, x_3, ...$
```math
\hat{y}=\begin{bmatrix}
x_{1}\\
x_{2}\\
x_{3}
\end{bmatrix}\begin{bmatrix}
w_{1} & w_{2} & w_{3}
\end{bmatrix} +b
```
- Typically minimizes mean squared error (MSE) $`\frac{1}{n}\sum\nolimits _{i=1}^{n}( y_{i} -\hat{y}_{i})^{2}`$ averaged over $n$ training samples via SGD.

For a linear model to work well, we must satisfy some conditions.
- Linearity: Independent and dependent variables have a linear relationship (as opposed to non-linear).
- Normality: Error (residuals) should follow a Gaussian distribution.
- No multicollinearity: Independent variables must be independent from each other.

## Logistic Regression
- Transform linear regression to classification by applying the sigmoid function which smoothly transforms $\hat{y}$ between 0 and 1.
```math
\hat{y}=\sigma\left(\begin{bmatrix}
x_{1}\\
x_{2}\\
x_{3}
\end{bmatrix}\begin{bmatrix}
w_{1} & w_{2} & w_{3}
\end{bmatrix} +b\right)
```
- For classification we need cross entropy loss $`-\sum _{j=1}^{k} y_{i,j}\log\hat{y}_{i,j}`$ where $k$ is the number of classes.
- Same conditions as linear regression except the dependent variable here is the **log-odds** or natural log of the odds for a class.

## Multi-layer Perceptron (MLP)
- Similar to linear regression, but a non-linear activation is added between layers to model non-linear relationships.

## Bias-Variance Tradeoff
- Overfitting is when a model achieves low bias, high variance.
- Underfitting is when a model achieves high bias, low variance.

## Regularization
- Ridge regression (**L2 norm**) is when we add a penalty term to the loss that is the square of the magnitude of coefficients. This results in coefficients that tend towards a range of 0 - 1.
- Lasso regression (**L1 norm**) is when we add a penalty term to the loss that is the absolute value of the magnitude of coefficients.  This results in sparse coefficients.
- **Dropout**

## Support Vector Machine (SVM)
<img src="https://miro.medium.com/v2/resize:fit:1400/1*ZpkLQf2FNfzfH4HXeMw4MQ.png" height="300">

- Uses labeled points in an $n$-dimensional feature space to find a hyperplane or classification boundary that maximizes the margin to the closest points of each class.
- Similar to linear classification with $\hat{y}_i=\text{sign}(w^Tx_i-b)$ and classes 1/-1.
- With a hard constraint $y_i(\hat{y}_i)=y_i(w^Tx_i-b)\geq1$, no points can be on the wrong side of the line. If we want to allow this, we adopt a softer constraint $y_i(w^Tx_i-b)\geq1-\epsilon$.

<img src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*mCwnu5kXot6buL7jeIafqQ.png" height="300">

- SVMs can also model a non-linear relationship by performing a non-linear transformation $\phi(x,y)$ of the original features.
- In the above picture, each point on a flat surface was mapped onto a curved surface. $\phi(x,y)=x^2+y^2$
- The **kernel trick** allows you to bypass the need for specifying this nonlinear transformation explicitly. Instead, you specify a "kernel"  function that directly describes how each points relate to each other.
  - This works because SVM only needs the dot product between two transformed points $\phi(x_1,y_1)\cdot\phi(x_2,y_2)$ and not each individual transformed $\phi(x,y)$.

## K-Means Clustering

<img src="https://stanford.edu/~cpiech/cs221/img/kmeansViz.png" height="300">

- Given a set of unlabeled points in feature space, we want to find clusters where the points of each cluster are similar.
- Initially, we pick $k$ points as centroids (centers of the cluster). Then we form $k$ clusters by assigning each point to its nearest centroid. Then we update the centroids by taking the mean of all points in each cluster. Repeat until convergence.
- Note that initial centroids matters significantly, so it is common practice to run K-Means++ multiple times to get the best convergence.
- Can also apply **kernel trick** if desired clusters are not initally linearly seperable.

## Principal Component Analysis (PCA)
- The goal with PCA is to reduce high dimensional features into a lower dimension while preserving information, ensuring that remaining features are vital and independent of each other.
- PCA identifies a set of orthogonal axes, called principal components, that captures the maximum variance in the data. It assumes that variance = information.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230420165431/Principal-Componenent-Analysisi.webp" height="300">

- In the above picture, there is more variance along axes $PC_1$, so it is chosen as the final 1D space over $PC_2$.
- Note that PCA does not give us a subset of the features that are useful. We don't know if area or radius was a more useful feature.

## Naive Bayes

- Let's say we want to find a classifier that can predict a label $Y\in\{0,1\}$ given some features $X_1,~X_2$.
- From a probabilistic perspective, we can say we want to estimate $P(Y=y|X_1=x_1~\text{and}~X_2=x_2)$ where $x_1$ and $x_2$ are our features for this sample.
- Using Bayes' theorem (below), we can express $P(Y|X)$ in terms of $P(X|Y),~P(Y),~P(X)$ which we can compute by looking at the probabilites in our training dataset.
```math
P(Y|X)=\frac{P(X|Y)P(Y)}{P(X)}
```
- By comparing the probabilities of the two labels, we can decide by choosing the higher one. Since $P(X)$ appears in both, we can just ignore it for our comparison.
```math
P(Y=0|X_1=x_1~\text{and}~X_2=x_2)\propto\frac{P(X_1=x_1~\text{and}~X_2=x_2|Y=0)P(Y=0)}{\enclose{horizontalstrike}{P(X)}}
```
```math
P(Y=1|X_1=x_1~\text{and}~X_2=x_2)\propto\frac{P(X_1=x_1~\text{and}~X_2=x_2|Y=1)P(Y=1)}{\enclose{horizontalstrike}{P(X)}}
```
- However, note that we need $P(X_1=x_1~\text{and}~X_2=x_2|Y=y)$ which is based on the probability we find in the dataset. If there aren't many occurrences of this case to count, the probability becomes unreliable.
- Thus, Naive Bayes assumes that each feature $X_1,~X_2$ are **independent** of each other, just as two coin flips may be independent of each other (**Big assumption!**). This separates the conditional so that we have a larger sample size for each.
```math
P(X_1=x_1~\text{and}~X_2=x_2|Y=y)=P(X_1=x_1|Y=y)P(X_1=x_1|Y=y)
```
- As expected, we also assume that the amount of training data is sufficient to model the probability properly.

## Decision Tree

## Transformers