# Machine Learning Basics

## K-Nearest Neigbors (KNN)

![Visualization](https://media.geeksforgeeks.org/wp-content/uploads/20231207103856/KNN-Algorithm-(1).png)

- Given a set of labeled data points, when encountering an unlabeled test data point, we can accurately label it by finding its "nearest neighbor" in the points we already know.
- Consider top k nearest neighbors when labeling, majority vote.
- The top k nearest neighbors are determined by a chosen distance metric: Euclidean, Manhattan, Minknowski.
- Can also perform regression by averaging the target values obtained from top k nearest neighbors.

## K-Means Clustering

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


## Transformers