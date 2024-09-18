# Machine Learning

## K-Nearest Neigbors (KNN)

![Visualization](https://media.geeksforgeeks.org/wp-content/uploads/20231207103856/KNN-Algorithm-(1).png)

- Given a set of labeled data points, when encountering an unlabeled test data point, we can accurately label it by finding its "nearest neighbor" in the points we already know.
- Consider top k nearest neighbors when labeling, majority vote.
- The top k nearest neighbors are determined by a chosen distance metric: Euclidean, Manhattan, Minknowski.
- Can also perform regression by averaging the target values obtained from top k nearest neighbors.

## K-Means Clusterings

## Linear Regression
- Fits a linear model for dependent variable $y$ and potentially multiple independent variables $x_1, x_2, x_3, x_n, ...$
$$y=\begin{bmatrix}
x_{1}\\
x_{2}\\
x_{3}
\end{bmatrix}\begin{bmatrix}
w_{1} & w_{2} & w_{3}
\end{bmatrix} +b$$

## Transformers