---
layout: essay
type: essay
title: Notes on An Introduction to Statistical Learning
date: 2020-05-12
labels:
  - Statistics
  - Machine Learning
  - Notes
---

<em>An Introduction to Statistical Learning, notes... </em>

<b>Motivation</b>: some notes on reviewing an Introduction to Statistical Learning (ISL) by Gareth James, Daniela Witten, Trevor Hastie, and Robert Tibshirani. The book is freely available <a href="http://faculty.marshall.usc.edu/gareth-james/ISL/" target="_blank">here</a>. `

## Chapter 2: Statistical Learning:
Statistical learning refers to a set of tools for understanding data and recognising patterns. In the case of *supervised* learning the goal is to predict an output or make a decision without explicit rule based programming but to use labeled input data to learn patterns. In contrast, *unsupervised* learning attempts to find patterns in data without pre-existing labels.

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y = f(X) %2B \epsilon">
</p>

There is a relationship between a response <img src="https://render.githubusercontent.com/render/math?math=Y"> and a set of <img src="https://render.githubusercontent.com/render/math?math=X"> predictors <img src="https://render.githubusercontent.com/render/math?math=(x_1, x_2, x_3, ..., x_p)">, with <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> being a random error term with a mean of zero. Statistical learning can be used to estimate the mapping between the response (dependent variable) and the predictors.

Statistical learning aims to best approximate the mapping function <img src="https://render.githubusercontent.com/render/math?math=f"> between the response (dependent variable) and the predictors. In general, an estimation of <img src="https://render.githubusercontent.com/render/math?math=f">, denoted by <img src="https://render.githubusercontent.com/render/math?math=\hat{f}">, will not be perfect and will introduce error. The error between <img src="https://render.githubusercontent.com/render/math?math=f"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{f}"> has a *reducible error* component that is reduced by better approximating the mapping function <img src="https://render.githubusercontent.com/render/math?math=\hat{f}">, and an irreducible component due to the error term <img src="https://render.githubusercontent.com/render/math?math=\epsilon">.
 

The two main motivations for learning this mapping are *prediction* and *inference*, where:

 - **Prediction**, in the case where the inputs <img src="https://render.githubusercontent.com/render/math?math=X"> are available, and since the error term averages to zero we predict as <img src="https://render.githubusercontent.com/render/math?math=\hat{Y} = \hat{f}(X)">, in many cases the exact form of <img src="https://render.githubusercontent.com/render/math?math=\hat{f}"> is not of conern.
 
 - **Inference**, is used to understand the way in which <img src="https://render.githubusercontent.com/render/math?math=Y"> is affected as <img src="https://render.githubusercontent.com/render/math?math=X_1, X_2, ... X_p"> change. To answer questions such as: which predictors are associated with the response, or what is th relationship between the response and each predictor?

Approaches to estimate <img src="https://render.githubusercontent.com/render/math?math=f"> share certain characteristics and can broadly be deemed *parametric* or *non-parametric*:

-  **parametric** - make an assumption about the functional nature, or shape, of <img src="https://render.githubusercontent.com/render/math?math=f">. For example, assume that <img src="https://render.githubusercontent.com/render/math?math=f"> is linear, yielding a linear model. Then estimate the set of parameters. In general, it is much simpler to estimate a set of parameters than it is to estimate an entirely arbitrary function <img src="https://render.githubusercontent.com/render/math?math=f">. A disadvantage of this approach is that the specified model won’t usually match the true form of <img src="https://render.githubusercontent.com/render/math?math=f">.

- **non-parametric** methods do not make explicit assumptions about the functional form of <img src="https://render.githubusercontent.com/render/math?math=f">. They are more flexible and can fit to a wider range of forms of <img src="https://render.githubusercontent.com/render/math?math=f">. The downside of this is that they often require many parameters to fit to <img src="https://render.githubusercontent.com/render/math?math=f">.

*supervised* or *unsupervised*, where:
- **supervised learning** refers to those scenarios in which for each observation of the predictor measurements there is an associated response measurement. The model generated relates the predictors to the response with the goal of accurately predicting future observations or of better inferring the relationship between the predictors and the response.

- **unsupervised learning** refers to those scenarios in which for each observation of the predictor measurements, there is no associated response. There is no response variable that can supervise the analysis that goes into generating a model. Often unsupervised learning involves *cluster analysis*, a process by which observations are arranged into relatively distinct groups.

*regression* or *classification*, where:

- **regression** problems have output variables that take on quantitative continuous values.

- **classification** problems have outputs that whose values are distinct classes or categories. Problems with a qualitative response are often referred to as classification problems.

**Quality of fit** is a way to asses the performance of a model used to solve a regression problem determining how well predictions match the observed data. A typical metric for this is the mean squared error (MSE), given as,

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{f}(x_i))^2">
</p>

where <img src="https://render.githubusercontent.com/render/math?math=\hat{f}(x_i)"> is the prediction given on the <img src="https://render.githubusercontent.com/render/math?math=i">th observation.  We would like to choose a model that has as low a mean-squared error on the test group as possible.

The **flexibility** or number of **degrees of freedom** of a model quantifies the number of parameters in the model that are free to vary. The degrees offreedom is a quality that summarizes the flexibility of a curve. As the number of degrees of freedom of a model increases the training MSE will usually decrease, whilst the test MSE may not. When the training MSE is small but the test MSE is large, the model is described as overfitting the data. Almost always the training MSE will be less than the test MSE because most methods aim to minimize the training MSE.

The expected test MSE for a given value <img src="https://render.githubusercontent.com/render/math?math=x_0"> can be decomposed into the sum of three quantities. The variance of <img src="https://render.githubusercontent.com/render/math?math=\hat{f}(x_0)">, the squared bias of <img src="https://render.githubusercontent.com/render/math?math=\hat{f}(x_0)">, and the variance of the error term, <img src="https://render.githubusercontent.com/render/math?math=\epsilon">. Formally, the balance of these opposing forces known as the **bias-variance tradeoff** can be written as follows:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=E (y_0 - \hat{f}(x_0))^2 = Var(\hat{f}(x_0)) %2B [Bias(\hat{f}(x_0))]^2  %2B  Var(\epsilon)">
</p>

to minimise the expected test error, a method should minimise both the variance and the bias. It can be seen that the expected test mean squared error can never be less than <img src="https://render.githubusercontent.com/render/math?math=Var(\epsilon)"> the irreducible error. Variance refers to the amount by which <img src="https://render.githubusercontent.com/render/math?math=\hat{f}"> would change if it were estimated using a different training data set. In general, more flexible methods have higher variance, bias refers to the error that is introduced by approximating a potentially complex function using a simple model. More flexible models tend to have less bias. In general, the more flexible the statistical learning method, the more variance will increase and bias decrease.

In the classification setting the quality of fit can be assessed looking at the training error. The training error rate is the proportion of errors that are made when applying <img src="https://render.githubusercontent.com/render/math?math=\hat{f}"> to the training observations. Formally stated as,

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\frac{1}{n}\sum_{i=1}^{n}I(y_i \neq \hat{y}_i)">
</p>

where <img src="https://render.githubusercontent.com/render/math?math=I"> is an indicator variable that equals 0 when <img src="https://render.githubusercontent.com/render/math?math=y = \hat{y}"> and equals 1 when <img src="https://render.githubusercontent.com/render/math?math=y \neq \hat{y}">. In simple terms, the error rate is the ratio of incorrect classifications to the observation count. As in the regression scenario, a good classifier is one for which the test error rate is smallest.

The **Bayes classifier** is a simple classifier that assigns each observation the most likely class, which on average minimises the test error rate given its predictor variables. In Bayesian terms, a test observation should be classified for the predictor vector <img src="https://render.githubusercontent.com/render/math?math=x_0"> to the class <img src="https://render.githubusercontent.com/render/math?math=j"> for which,

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Pr(Y=j|X=x_0)">
</p>

is largest. That is, the class for which the conditional probability that <img src="https://render.githubusercontent.com/render/math?math=Y=j">
 , given the observed predictor vector <img src="https://render.githubusercontent.com/render/math?math=x_0">, is largest. This classifier is called the Bayes classifier.

In a two-class scenario, this can be stated as  <img src="https://render.githubusercontent.com/render/math?math=Pr(Y=1|X=x_0) > 0.5"> matching class A when true and class B when false. The threshold where the classification probability is exactly 50% is known as the Bayes decision boundary.

The Bayes classifier yields the lowest possible test error rate since it will always choose the class with the highest probability. The Bayes error rate can be stated formally as <img src="https://render.githubusercontent.com/render/math?math=1 - E(maxPr_j(Y=j|X)">. The Bayes error rate can also be described as the ratio of observations that lie on the "wrong" side of the decision boundary. Unfortunately, the conditional distribution of Y given X is often unknown, so the Bayes classifier is most often unattainable.

Many modelling techniques try to compute the conditional distribution of <img src="https://render.githubusercontent.com/render/math?math=Y"> given
<img src="https://render.githubusercontent.com/render/math?math=X"> and then provide estimated classifications based on the highest estimated probability. The **k-nearest neighbors classifier** is one such method.

The K-nearest neighbors classifier takes a positive integer K and first identifies the K points that are nearest to <img src="https://render.githubusercontent.com/render/math?math=x_0">, represented by <img src="https://render.githubusercontent.com/render/math?math=N_0">. It next estimates the conditional probability for class <img src="https://render.githubusercontent.com/render/math?math=j"> based on the fraction of points in <img src="https://render.githubusercontent.com/render/math?math=N_0"> who have a response equal to <img src="https://render.githubusercontent.com/render/math?math=j">. Formally, the estimated conditional probability can be stated as

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Pr(Y=j|X=x_0)= \frac{1}{K}\sum_{i{\epsilon}N_0}I(y_i=j)">
</p>

The K-Nearest Neighbor classifier then applies Bayes theorem and yields the classification with the highest probability. Despite its simplicity, the K-Nearest Neighbor classifier often yields results that are surprisingly close to the optimal Bayes classifier. The choice of K can have a drastic effect on the yielded classifier. Too low a K yields a classifier that is too flexible, has too high a variance, and low bias.

Conversely, as K increases, the yielded classifier becomes less flexible, with a low variance, but high bias. In both regression and classification scenarios, choosing the correct level of flexibility is critical to the success of the model.
