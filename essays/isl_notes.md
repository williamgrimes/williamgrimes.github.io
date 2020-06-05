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

#### Further reading:
* <a href="https://youtu.be/C3nIFH649wY" target="_blank"> Bias-Variance decomposition.</a>

## Chapter 3: Linear Regression:
*Simple linear regression* predicts a quantitative response  <img src="https://render.githubusercontent.com/render/math?math=Y"> from a single predictor variable <img src="https://render.githubusercontent.com/render/math?math=X">, assuming they are linearly related, formally:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y= \beta_0  %2B \beta_1X">
</p>

where 
<img src="https://render.githubusercontent.com/render/math?math=\beta_{0}"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_1">, are two unknown constants (parameters) representing the *intercept* and *slope* of the linear model. In practice these parameters are unknown and the goal of modelling with a linear regression is to find values of <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> that fit the data well. The most common approach to measure the *closeness* of the line to the data is using the *least squares* criterion. Assuming that for <img src="https://render.githubusercontent.com/render/math?math=i">:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\hat{Y}_i = \hat{\beta}_0  %2B \hat{\beta}_1X">
</p>

then the <img src="https://render.githubusercontent.com/render/math?math=i">th residual can be represented as the **residual sum of squares**:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=RSS = e^2_1 %2B e^2_2 %2B ... %2B e^2_n">
    or  
    <img src="https://render.githubusercontent.com/render/math?math=RSS = (y_1-\hat{\beta}_0-\hat{\beta}_1x_1)^2 %2B (y_2-\hat{\beta}_0-\hat{\beta}_1x_2)^2 %2B ... %2B (y_n-\hat{\beta}_0-\hat{\beta}_1x_n)^2">
</p>

assuming sample means of <img src="https://render.githubusercontent.com/render/math?math=\bar{y} = \frac{1}{n}\sum_{i=1}^{n}y_i">, and <img src="https://render.githubusercontent.com/render/math?math=\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i">.

calculus can be used (see further reading) to estimate the least squares coefficient estimates for linear regression minimising the residual sum of squares:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\beta_1 = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{(x_i - \bar{x})^2}">
    and
    <img src="https://render.githubusercontent.com/render/math?math=\beta_0 = \bar{y} - \hat{\beta_1} \bar{x}">
</p>

**How to assess coefficient estimate accuracy?** The model used by simple linear regression defines the population regression line, which describes the best linear approximation to the true relationship between <img src="https://render.githubusercontent.com/render/math?math=X"> and <img src="https://render.githubusercontent.com/render/math?math=Y"> for the population. A simple linear regression represents the relationship as:

<img src="https://render.githubusercontent.com/render/math?math=Y= \beta_0 %2B \beta_1X  %2B \epsilon">

where <img src="https://render.githubusercontent.com/render/math?math=\epsilon"> is the *irreducible error*, which is a catchall error term for what is missed by the simple model given that the relationship is probably not linear, and their maybe other input variables affecting the response, this term is assumed to be independent of <img src="https://render.githubusercontent.com/render/math?math=X">.

The coefficient estimates yielded by least squares regression characterize the least squares line,

<img src="https://render.githubusercontent.com/render/math?math=\hat{Y}= \hat{\beta_0} %2B \hat{\beta_1}X_i">

The difference between the population regression line and the least squares line is similar to the difference that emerges when using a sample to estimate the characteristics of a population.

In linear regression, the unknown coefficients, <img src="https://render.githubusercontent.com/render/math?math=\beta_0"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> define the population regression line, whereas the estimates of those coefficients, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> define the least squares line.

Parameter estimates for a sample may overestimate or underestimate the value of a particular parameter, but an unbiased estimator does not systemically overestimate or underestimate the true parameter. This means that using an unbiased estimator and a large number of data sets, the values of the coefficients <img src="https://render.githubusercontent.com/render/math?math=\beta_0"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> could be determined by averaging the coefficient estimates from each of those data sets.

The standard error can be used to estimate the accuracy of a single estimated value, such as an average.

<img src="https://render.githubusercontent.com/render/math?math=Var(\hat{\mu}) = SE(\hat{\mu})^2 = \frac{\sigma^2}{n}">

where <img src="https://render.githubusercontent.com/render/math?math=\mu">, is the standard deviation of each <img src="https://render.githubusercontent.com/render/math?math=y_i">. The standard error describe approximately the amount that <img src="https://render.githubusercontent.com/render/math?math=\hat{\mu}"> differs from <img src="https://render.githubusercontent.com/render/math?math=\mu">. More observations gives a larger denominator n and a smaller standard error.

Standard errors for <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> are calculated as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=SE(\beta_0)^2 = \sigma^2 [ \frac{1}{n} %2B \frac{\bar{x}^2}{\sum{n}{i=1}(x_i - \bar{x})^2} ] ">
</p>
and,
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=SE(\beta_1)^2 = \frac{\sigma^2}{\sum_{n}^{i=1}(x_i - \bar{x})^2} ">
</p>

where 

<img src="https://render.githubusercontent.com/render/math?math=\sigma^2 = Var(\epsilon)"> and <img src="https://render.githubusercontent.com/render/math?math=\epsilon_i"> is not correlated with <img src="https://render.githubusercontent.com/render/math?math=\sigma^2">, 

which is usually not known but can be estimated from the data, known as the _residual standard error_ (RSE):

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=RSE = \sqrt{\frac{RSS}{(n - 2)}}">
</p>

where RSS is the residual sum of squares. Standard errors can be used to compute confidence intervals and prediction intervals. A confidence interval is defined as a range of values such that there’s a certain likelihood that the range will contain the true unknown value of the parameter. For simple linear regression the 95% confidence interval for <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> can be approximated by: <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1} \pm 2 \times SE(\hat{\beta_1})">. Similarly, for <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}">, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0} \pm 2 \times SE(\hat{\beta_0})">.

The accuracy of an estimated prediction depends on whether we wish to predict an individual response or the average response. When predicting an individual response, <img src="https://render.githubusercontent.com/render/math?math=y = f(x) %2B \epsilon">, a prediction interval is used. When predicting an average response, <img src="https://render.githubusercontent.com/render/math?math=f(x)"> a confidence interval is used.

Prediction intervals will always be wider than confidence intervals because they take into account the uncertainty associated with <img src="https://render.githubusercontent.com/render/math?math=\epsilon">, the irreducible error.

The standard error can also be used to perform hypothesis testing on the estimated coefficients. The most common hypothesis test called the **t-test**  involves testing the null hypothesis _H0_ against the hypothesis _H1_, stated as:

- _H0: There is no relationship between X and Y_, 
- _H1: There is some relationship between X and Y._

In mathematical terms, the null hypothesis corresponds to testing if <img src="https://render.githubusercontent.com/render/math?math=\beta_1 = 0">, which reduces to

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=y = \beta_0 %2B \epsilon">,
</p>

in other words this tests that X is not related to Y.
To test the null hypothesis, it is necessary to determine whether the estimate of <img src="https://render.githubusercontent.com/render/math?math=\beta_1">, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}">, is sufficiently far from zero to provide confidence that <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> is non-zero.

What is close enough depends on <img src="https://render.githubusercontent.com/render/math?math=SE(\hat{\beta_1})">. When <img src="https://render.githubusercontent.com/render/math?math=SE(\hat{\beta_1})"> is small, then small values of <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> may provide strong evidence that <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> is not zero. Conversely, if <img src="https://render.githubusercontent.com/render/math?math=SE(\hat{\beta_1})">. When <img src="https://render.githubusercontent.com/render/math?math=SE(\hat{\beta_1})"> is large, then <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> will need to be large in order to reject the null hypothesis.

In practice, computing a **t-statistic**, which measures the number of standard deviations that <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}">, is away from 0, is useful for determining if an estimate is sufficiently significant to reject the null hypothesis. The _t-Statistic_ is computed as follows:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=t = \frac{\hat{\beta_1} - 0}{SE(\hat{\beta_1})}">
</p>

If there is no relationship between X and Y, it is expected that a t-distribution with n−2 degrees of freedom should be yielded.

With such a distribution, it is possible to calculate the probability of observing a value of <img src="https://render.githubusercontent.com/render/math?math=|t|"> or larger assuming that <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1} = 0">. This probability, called the **p-value**, can indicate an association between the predictor and the response if sufficiently small.

**How to assess model accuracy?** Having rejected the null hypothesis, it is often useful to quantify the goodness of fit of the model (the extent to which the model fits the data). For a linear regression model typically the **residual standard error** along with the **r-squared** statistic.

The residual standard error is an estimate of the standard deviation of <img src="https://render.githubusercontent.com/render/math?math=\epsilon">, the irreducible error. In other words the RSE is the average amount by which the response will deviate from the true regression line. The residual standard error can be computed as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=RSE = \sqrt{\frac{1}{n-2}RSS} =\sqrt{\frac{1}{n-2}\sum_{i=1}^{n}(y_i - \hat{y_i})^2}">
</p>

The residual standard error is a measure of the lack of fit of the model to the data. A large value indicates the model does not fit the data well. A difficulty using the residual standard error however is that the magnitude is in units of Y so determining a good RSE value is not intuitive.

The  statistic is an alternative measure of fit that takes the form of a proportion. The R2 statistic captures the proportion of variance explained as a value between 0 and 1, independent of the unit of Y.

The <img src="https://render.githubusercontent.com/render/math?math=R^2"> statistic provides a measure of fit as a proportion of variance explained as a value between 0 and 1. It is calculated as follows:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=R^2 = \frac{TSS - RSS}{TSS} = 1 - \frac{RSS}{TSS}">
</p>

where <img src="https://render.githubusercontent.com/render/math?math=RSS = \sum_{i=1}^{n}(y_i - \hat{y_i})^2">, and <img src="https://render.githubusercontent.com/render/math?math=TSS = \sum_{i=1}^{n}(y_i - \bar{y_i})^2">.

The total sum of squares, TSS, measures the total variance in the response Y. The TSS can be thought of as the total variability in the response before applying linear regression. Conversely, the residual sum of squares, RSS, measures the amount of variability left after performing the regression. Ergo, TSS−RSS measures the amount of variability in the response that is explained by the model. An r-squared value close to 1 indicates that a large proportion of the bariability in the response is explained by the model, conversely a value close to 0 indicates that the model accounted for very little of the variability. 

An r-squared value close to 0 may be because the linear model is a bad assumption or because the standard deviation (squared) is high. Although r-squared is easy to interpret as it is confined between 0 and 1, determining what constitutes an acceptable r-squared is non-trivial and depends on the specifics of the problem.

**Correlation** is another measure of the linear relationship between X and Y, calculated as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Cor(X, Y) = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i-1}{n}(x_i - \bar{x})^2}\sqrt{\sum_{i-1}{n}(y_i - \bar{y})^2}}">
</p>

This suggests that <img src="https://render.githubusercontent.com/render/math?math=r=Cor(X, Y)"> could be used instead of r-squared to assess the goodness of fit for a linear model. Correlation does not extend to multiple linear regression since correlation quantifies the association between a single pair of variables, however the r-squared statistic can.

**Multiple linear regression** models extend simple linear regression to accommodate multiple predictors in the form:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y= \beta_0 %2B \beta_1X_1 %2B \beta_2X_2 %2B ... %2B \beta_pX_p">
</p>

As the coefficients <img src="https://render.githubusercontent.com/render/math?math=\beta_0, \beta_1, \beta_2, %2B ... %2B \beta_p"> are not known, it is necessary to estimate their values <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}, \hat{\beta_1}, \hat{\beta_2}, %2B ... %2B \hat{\beta_p}"> giving:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y= \hat{\beta_0} %2B \hat{\beta_1}X_1 %2B \hat{\beta_2}X_2 %2B ... %2B \hat{\beta_p}X_p">
</p>

The coefficients can be estimated using the same least squares approach as in simple linear regression, to minimise the sum of squares, using matrix algebra:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=RSS = \sum_{i=1}^{n}(y_i - \hat{y_i})^2 = \sum_{i=1}^{n}(y_i - \hat{\beta_0} %2B \hat{\beta_1}X_1 %2B \hat{\beta_2}X_2 %2B ... %2B \hat{\beta_p}X_p)^2">
</p>

**Coefficient accuracy is assessed in multiple regressions** by testing the null hypothesis _H0_ against the hypothesis _H1_, stated as:

- _H0_: <img src="https://render.githubusercontent.com/render/math?math=H_0 : \beta_1 = \beta_2 = ... = \beta_p = 0">
- _H1_: <img src="https://render.githubusercontent.com/render/math?math=H_a: at least one of B_j \neq 0 ">

Here the **F-statistic** can be used to determine which hypothesis is true, and is computed as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=F = \frac{(TSS - RSS)/p}{RSS/(n - p - 1)} = \frac{\frac{TSS - RSS}{p}}{\frac{RSS}{n - p - 1}}">
</p>

where again,  <img src="https://render.githubusercontent.com/render/math?math=RSS = \sum_{i=1}^{n}(y_i - \hat{y_i})^2">, and <img src="https://render.githubusercontent.com/render/math?math=TSS = \sum_{i=1}^{n}(y_i - \bar{y_i})^2">..

If the assumptions of the linear model, represented by the alternative hypothesis, are true it can be shown that:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=E\{\frac{RSS}{n - p - 1}\} = \sigma^{2}">
</p>

and conversely for the null-hypothesis if true, it can be shown that:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=E\{\frac{TSS - RSS}{p}\} = \sigma^{2}">
</p>

When there is no relationship between the response and the predictors the _F-statisitic_ has a value close to 1, and conversely, if the alternative hypothesis is true, then the _F-statistic_ will take on a value greater than 1. When n is large, an F-statistic only slightly greater than 1 may provide evidence against the null hypothesis. If n is small, a large _F-statistic_ is needed to reject the null hypothesis.

When the null hypothesis is true and the errors <img src="https://render.githubusercontent.com/render/math?math=\epsilon_i"> have a normal distribution, the _F-statistic_ follows an _F-distribution_. Using the _F-distribution_, it is possible to figure out a _p-value_ for the given _n_, _p_, and _F-statistic_. Based on the obtained _p-value_, the validity of the null hypothesis can be determined.

It is sometimes desirable to test that a particular subset of _q_ coefficients are 0. This equates to a null hypothesis of

- _H0_: <img src="https://render.githubusercontent.com/render/math?math=H_0 : \beta_{p-q+1} = \beta_{p-q+2} = ... = \beta_{p} = 0">

Supposing that the residual sum of squares for such a model is <img src="https://render.githubusercontent.com/render/math?math=RSS_0"> then the F-statistic could be calculated as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=F = \frac{(RSS_0 - RSS)/q}{RSS/(n - p - 1)} = \frac{\frac{RSS_0 - RSS}{q}}{\frac{RSS}{n - p - 1}}">
</p>

Even in the presence of p-values for each individual variable, it is still important to consider the overall F-statistic because there is a reasonably high likelihood that a variable with a small p-value will occur just by chance, even in the absence of any true association between the predictors and the response.

In contrast, the F-statistic does not suffer from this problem because it adjusts for the number of predictors. The F-statistic is not infallible and when the null hypothesis is true the F-statistic can still result in p-values below 0.05 about 5% of the time regardless of the number of predictors or the number of observations.

The F-statistic works best when p is relatively small or when p is relatively small compared to n.
When p is greater than n, multiple linear regression using least squares will not work, and similarly, the F-statistic cannot be used either.

**Selecting important variables** is the next step after establishing that at least one of the predicotrs is associated with the response. _Variable selection_ is the process of removing extraneous predictors that don't relate to the response.

An exhaustive search would test different subsets of predictors and selecting the best model as determined by various statistical methods. However, there are <img src="https://render.githubusercontent.com/render/math?math=2^p"> subset of predictors so this is often infeasible. An efficient and automated means of choosing a smaller subset of models is needed, there are a number of approaches to limiting the range of possible models:

* _Forward selection_ is a greedy approach starting with a model having an intercept but no predictors, and attempts to add predictors and perform linear regressions, keeping whichever predictor results in the lowest residual sum of squares. The predictor yielding the lowest RSS is added to the model one-by-one until some halting condition is met.
* _Backward selection_ begins with a model having all the predictors and proceeds to remove variables with the highest p-value each iteration until some stopping condition is met. Backwards selection cannot be used when p>n.
* _Mixed selection_ starts with a null model and, repeatedly adds whichever predictor yields the best fit. As more predictors are added, the p-values become larger. When this happens, if the p-value for one of the variables exceeds a certain threshold, that variable is removed from the model. The selection process continues in this forward and backward manner until all the variables in the model have sufficiently low p-values and all the predictors excluded from the model would result in a high p-value if added to the model.

In addition to r-squared and RSE, it is also useful to plot the data to verify the model. However, it is important to note that these predictions will be subject to three types of uncertainty:

1. The coefficient estimates, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}, \hat{\beta_1}, ..., , \hat{\beta_p}">, are only estimates of the actual coefficients <img src="https://render.githubusercontent.com/render/math?math=\beta_0, \beta_1, ..., , \beta_p">. The error introduced by this inaccuracy is reducible error and a confidence interval can be computed to determine how close <img src="https://render.githubusercontent.com/render/math?math=\hat{y}"> is to f(X).
2. The assumption of a linear model for f(X) is almost always an approximation of reality, which means additional reducible error is introduced due to model bias. A linear model often models the best linear approximation of the true, non-linear surface. 
3. Even in the case where f(X) and the true values of the coefficients are known, the response value cannot be predicted exactly because of the random, irreducible error <img src="https://render.githubusercontent.com/render/math?math=\epsilon">.

**Qualitative predictors** can also be accommodated in  linear regression by introducing an indicator (dummy) variable, that takes a numerical encoding, as follows:
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=X_i = \big\{ \begin{array}{cc}{1\quad if\quad p_i = class \A}\\{0\quad if\quad p_i = class \B}\end{array}">
</p>
this yields a regression equation as:
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=y_i = \beta_0 %2B \beta_1 X_1 %2B \epsilon_i = \big\{ \begin{array}{cc}{\beta_0 %2B \beta_1 %2B \epsilon_i  \quad if\quad p_i = class \A}\\{\beta_0 %2B \epsilon_i \quad if\quad p_i = class \B}\end{array}">
</p>

Given such a coding, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> represents the average difference in  <img src="https://render.githubusercontent.com/render/math?math=X_1"> between classes A and B.

When a qualitative predictor takes on more than two values, a single dummy variable cannot represent all possible values. Instead, multiple dummy variables can be used. The number of variables required will always be one less than the number of values that the predictor can take on.

For example, with a predictor that can take on three values, the following coding could be used

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=X_{i1} = \big\{ \begin{array}{cc}{1\quad if\quad p_i = class \A}\\{0\quad if\quad p_i \ne class \A}\end{array}">
</p>
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=X_{i2} = \big\{ \begin{array}{cc}{1\quad if\quad p_i = class \B}\\{0\quad if\quad p_i \ne class \B}\end{array}">
</p>
this yields a regression equation as:
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=y_i = \beta_0 %2B \beta_1 X_1  %2B \beta_2 X_2 %2B \epsilon_i = \big\{ \begin{array}{cc}{\beta_0 %2B \beta_1 %2B \epsilon_i  \quad if\quad p_i = class \A}\\{\beta_0 %2B \beta_2  %2B \epsilon_i \quad if\quad p_i = class \B}\\{\beta_0 %2B \epsilon_i \quad if\quad p_i = class \C}\end{array}">
</p>

With such a coding, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}"> can be interpreted as the average response for class C. <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> can be interpreted as the average difference in response between classes A and C. Finally, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_2}"> can be interpreted as the average difference in response between classes B and C.

The case where <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_1}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_2}"> are both zero, the level with no dummy variable, is known as the baseline.

Using dummy variables allows for easily mixing quantitative and qualitative predictors. There are many ways to encode dummy variables. Each approach yields equivalent model fits, but results in different coefficients and different interpretations that highlight different contrasts.

**Predictor interactions and extending the linear model**, restrictive assumptions are made in linear regressions. Principally the _additive assumption_ which assumes that the relationship between the predictors and response is additive, another assumption is that the relationship between the predictors and the response is linear.

An additive assumption implies that the effect of changes in a predictor on the response is independent of the other predictors, which is often not the case. A linear assumption implies that the change in the response due to a change in predictor is constant. **Interaction terms** can be added to overcome the limitations of the additive model, for example:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y = \beta_0  %2B \beta_1 X_1 %2B \beta_2 X_2 %2B \beta_3 X_1 X_2 %2B \epsilon">
</p>

The hierarchical principle states that, when an interaction term is included in the model, the main effects should also be included, even if the p-values associated with their coefficients are not significant. The reason for this is that  <img src="https://render.githubusercontent.com/render/math?math=X_1 X_2"> is often correlated with <img src="https://render.githubusercontent.com/render/math?math=X_1"> and  <img src="https://render.githubusercontent.com/render/math?math=X_2"> and removing them tends to change the meaning of the interaction.

If  <img src="https://render.githubusercontent.com/render/math?math=X_1 X_2"> is related to the response, then whether or not the coefficient estimates of <img src="https://render.githubusercontent.com/render/math?math=X_1"> or <img src="https://render.githubusercontent.com/render/math?math=X_2"> are exactly zero is of limited interest.

Interaction terms can also model a relationship between a quantitative predictor and a qualitative predictor.

**Non-Linear relationships** can be modelled to mitigate the effects of the linear assumption by incorporating polynomial functions of the predictors in the regression model. For example, in a scenario where a quadratic relationship seems likely, the following model could be used

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Y = \beta_0  %2B \beta_1 X_1 %2B \beta_2 X_1^2 %2B \epsilon">
</p>

This extension of the linear model to accommodate non-linear relationships is called **polynomial regression**.

**Problems with linear regression:**

1. **Non-linearity**: If the true relationship between the response and predictors is far from linear, then virtually all conclusions that can be drawn from the model are suspect and prediction accuracy can be significantly reduced. **Residual plots** are useful for identifying non-linearity. 

2. **Correlation of error terms**: An important assumption of linear regression is that the error terms, are uncorrelated. If the error terms are correlated it will result in incorrect standard error values that will tend to underestimate the true standard error. This will result in prediction intervals and confidence intervals that are narrower than they should be. In addition, p-values associated with the model will be lower than they should be. In other words, correlated error terms can make a model appear to be stronger than it really is. Correlations in error terms can be the result of time series data, unexpected observation relationships, and other environmental factors. Observations that are obtained at adjacent time points will often have positively correlated errors. Good experimental design is a crucial factor in limiting correlated error terms.

3. **Non-constant variance of error terms**: linear regression also assumes that the error terms have a constant variance,

    <p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Var(\epsilon_i_) = \sigma^2">
    </p>
    Standard errors, confidence intervals, and hypothesis testing all depend on this assumption.

4. **Outliers** an outlier is an example for which yi is far from the value predicted by the model. Excluding outliers can result in improved residual standard error and improved r-squared values, usually with negligible impact to the least squares fit.

    Residual plots can help identify outliers, though it can be difficult to know how big a residual needs to be before considering a point an outlier. To address this, it can be useful to plot the studentized residuals instead of the normal residuals. Studentized residuals are computed by dividing each residual, <img src="https://render.githubusercontent.com/render/math?math=\epsilon_i">, by its estimated standard error. Observations whose studentized residual is greater than |3| are possible outliers.

    Outliers should only be removed when confident that the outliers are due to a recording or data collection error since outliers may otherwise indicate a missing predictor or other deficiency in the model.

5. **High-leverage points** While outliers relate to observations for which the response yi is unusual given the predictor xi, in contrast, observations with high leverage are those that have an unusual value for the predictor xi for the given response yi.

    High leverage observations tend to have a sizable impact on the estimated regression line and as a result, removing them can yield improvements in model fit.

    For simple linear regression, high leverage observations can be identified as those for which the predictor value is outside the normal range. With multiple regression, it is possible to have an observation for which each individual predictor’s values are well within the expected range, but that is unusual in terms of the combination of the full set of predictors.

    To qualify an observation’s leverage, the leverage statistic can be computed.

6. **Collinearity** refers to the situation in which two or more predictor variables are closely related to one another. Collinearity can pose problems for linear regression because it can make it hard to determine the individual impact of collinear predictors on the response.

    Collinearity reduces the accuracy of the regression coefficient estimates, which in turn causes the standard error of <img src="https://render.githubusercontent.com/render/math?math=\beta_j"> to grow. Since the T-statistic for each predictor is calculated by dividing <img src="https://render.githubusercontent.com/render/math?math=\beta_j"> by its standard error, collinearity results in a decline in the true T-statistic. This may cause it to appear that <img src="https://render.githubusercontent.com/render/math?math=\beta_j"> and <img src="https://render.githubusercontent.com/render/math?math=x_j"> are related to the response when they are not. As such, collinearity reduces the effectiveness of the null hypothesis. Because of all this, it is important to address possible collinearity problems when fitting the model.

    One way to detect collinearity is to generate a correlation matrix of the predictors. Any element in the matrix with a large absolute value indicates highly correlated predictors. This is not always sufficient though, as it is possible for collinearity to exist between three or more variables even if no pair of variables have high correlation. This scenario is known as multicollinearity.

    Multicollinearity can be detected by computing the variance inflation factor. The variance inflation factor is the ratio of the variance of <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_j}"> when fitting the full model divided by the variance of <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_j}"> if fit on its own. The smallest possible VIF value is 1.0, which indicates no collinearity whatsoever. In practice, there is typically a small amount of collinearity among predictors. As a general rule of thumb, VIF values that exceed 5 or 10 indicate a problematic amount of collinearity.
    
**Parametric methods versus non-parametric methods**. A non-parametric method akin to linear regression is k-nearest neighbors regression which is closely related to the k-nearest neighbors classifier. A parametric approach will outperform a non-parametric approach if the parametric form is close to the true form of f(X). The choice of a parametric approach versus a non-parametric approach will depend largely on the bias-variance trade-off and the shape of the function f(X).
When the true relationship is linear, it is difficult for a non-parametric approach to compete with linear regression because the non-parametric approach incurs a cost in variance that is not offset by a reduction in bias. Additionally, in higher dimensions, K-nearest neighbors regression often performs worse than linear regression. This is often due to combining too small an n with too large a p, resulting in a given observation having no nearby neighbors. This is often called the **curse of dimensionality**.

As a general rule, parametric models will tend to outperform non-parametric models when there are only a small number of observations per predictor.
    

#### Further reading:
* <a href="https://medium.com/@erika.dauria/looking-at-r-squared-721252709098" target="_blank">Looking at r-squared.</a>
* <a href="https://math.stackexchange.com/questions/63238/why-do-we-use-a-least-squares-fit" target="_blank">Why do we use a least squuares fit?</a>.
* <a href="https://youtu.be/ewnc1cXJmGA" target="_blank">Deriving the least squares estimators of the slope and intercept.</a>
* <a href="https://youtu.be/rODUBTRUV0U" target="_blank">Deriving the mean and variance of the least squares slope estimator in simple linear regression</a>

## Chapter 4: Classification:
Linear regression is an apt classifier in the scenario of binary qualitative responses, however beyond two levels difficulties arise. The choice of coding scheme is problematic, with different coding schemes yielding different predictions.

**Logistic regression** models the probability that <img src="https://render.githubusercontent.com/render/math?math=y"> belongs to a particular category (not the response itself). The _logistic function_ ensures the prediction is between 0 and 1, and is given as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=p(X) = \frac{e^{\beta_0 %2B \beta_1 X}}{1 %2B  e^{\beta_0 %2B \beta_1 X}}">
</p>

after re-balancing:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\frac{p(X)}{1 - p(X)} =e^{\beta_0 %2B \beta_1 X}">
</p>

The left side of the above equation is known as the odds and takes a value between zero and infinity. The _logit_ function or _log odds_ takes the logarithm of both sides:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=log \big[\frac{p(X)}{1 - p(X)} \big]=\beta_0 %2B \beta_1 X">
</p>

Logistic regression has a logit function that is linear in terms of X. Unlike linear regression where <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> represents the average change in Y with a one-unit increase in X, for logistic regression, increasing X by one-unit yields a <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> change in the log-odds which is equivalent to multiplying the odds by <img src="https://render.githubusercontent.com/render/math?math=\epsilon^{\beta_1}">.

The relationship between _p(X)_ and _X_ is not linear, so <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> does not correspond to the change in _p(X)_ given one-unit increase in _X_. However, if <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> is positive, increasing _X_ will be associated with an increase in _p(X)_ and, similarly, if <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> is negative, an increase in _X_ will be associated with a decrease in _p(X)_. How much change will depend on the value of _X_.

**Estimating regression coefficients** for logistic regression uses a strategy called **maximum likelihood**.

The maximum likelihood determines estimates for <img src="https://render.githubusercontent.com/render/math?math=\beta_0"> and <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> such that the predicted probability of <img src="https://render.githubusercontent.com/render/math?math=\hat{p}(x_i)"> corresponds with the observed classes as closely as possible. Formally, this yield an equation called a likelihood function:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\ell(\beta_0, \beta_1)) \displaystyle \prod_{i:y_{i}=1}p(X_{i})\times \displaystyle \prod_{j:y_{j}=0}(1-p(X_{j}))">
</p>

Estimates for <img src="https://render.githubusercontent.com/render/math?math=\beta_0"> and<img src="https://render.githubusercontent.com/render/math?math=\beta_1"> are chosen so as to maximize this likelihood function. Linear regression’s least squares approach is actually a special case of maximum likelihood.

Logistic regression measures the accuracy of coefficient estimates using a quantity called the **z-statistic**, which is similar to the t-statistic. The z-statistic for <img src="https://render.githubusercontent.com/render/math?math=\beta_1"> is represented by 

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\normalsize \textrm{z-statistic}(\beta_{1}) = \frac{\hat{\beta}_{1}}{\mathrm{SE}(\hat{\beta}_{1})}">
</p>

A large z-statistic supports the hypothesis, where in logistic regression, the null hypothesis is:

* _H0_: <img src="https://render.githubusercontent.com/render/math?math=\beta_1 = 0">
implies that

<img src="https://render.githubusercontent.com/render/math?math=p(X)=\frac{\epsilon^{\beta_0}}{1 %2B \epsilon^{\beta_0}}">

and, therefore, p(X) does not depend on X.

*Predictions with logistic regression* are made plugging in the estimates found from the maximum likelihood estimation in to the model equation

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\hat{p}(X) = \frac{e^{\hat{\beta_0} %2B \hat{\beta_1} X}}{1 %2B  e^{\hat{\beta_0} %2B \hat{\beta_1} X}}">
</p>

Generally the estimated intercept, <img src="https://render.githubusercontent.com/render/math?math=\hat{\beta_0}"> captures the ratio of positive and negative classifications in the given data set, and is not directly interpretable in most situations.

**Multiple logistic regression** is an extension of logistic regression with more predictors, that uses a strategy similar to that employed for linear regression, multiple logistic regression can be generalised as,

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=log \big[\frac{p(X)}{1 - p(X)} \big]=\beta_0 %2B \beta_1 X_1 %2B ... %2B \beta_p X_p">
</p>

The log-odds equation for multiple logistic regression can be expressed as

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=p(X)=\frac{\epsilon^{\beta_0 %2B \beta_1 X_1 %2B ... %2B \beta_p X_p}}{1 %2B \epsilon^{\beta_0 %2B \beta_1 X_1 %2B ... %2B \beta_p X_p}}">
</p>

Maximum likelihood is also used to estimate <img src="https://render.githubusercontent.com/render/math?math=\beta_0, \beta_1, ..., \beta_p"> in the case of multiple logistic regression.

In general, the scenario in which the result obtained with a single predictor does not match the result with multiple predictors, especially when there is correlation among the predictors, is referred to as **confounding**. More specifically, confounding describes situations in which the experimental controls do not adequately allow for ruling out alternative explanations for the observed relationship between the predictors and the response.

Though multiple-class logistic regression is possible, discriminant analysis tends to be the preferred means of handling multiple-class classification.

**Linear discriminant analysis (LDA)** is a technique to find a linear combination of features that characterizes or separates two or more classes of objects or events. The resulting combination may be used as a linear classifier, or, more commonly, for dimensionality reduction before later classification. 

Logistic regression models the conditional distribution of the response Y given the predictors X, whilst linear discriminant analysis takes the approach of modeling the distribution of the predictors X separately in each of the response classes , Y, and then uses Bayes’ theorem to invert these probabilities to estimate the conditional distribution.

Linear discriminant analysis is popular when there are more than two response classes. It has some advantages over logistic regression:
* The parameter estimates for logistic regression can be surprisingly unstable when the response classes are well separated. Linear discriminant analysis does not suffer from this problem.
* Logistic regression is more unstable than linear discriminant analysis when n is small and the distribution of the predictors X is approximately normal in each of the response classes.

Classification With Bayes’ Theorem
Assuming a qualitative variable Y that can take on <img src="https://render.githubusercontent.com/render/math?math=K \geq 2"> distinct, unordered values, the prior probability describes the probability that a given observation is associated with the kth class of the response variable Y.

The density function of X for an observation that comes from the kth class is defined as

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=f_k(X) = Pr(X=x|Y=k)">
</p>


This means that <img src="https://render.githubusercontent.com/render/math?math=f_k(X)"> should be relatively large if there’s a high probability that an observation from the kth class features X=x. Conversely, <img src="https://render.githubusercontent.com/render/math?math=f_k(X)"> will be relatively small if it is unlikely that an observation in class k would feature X=x.

Following this intuition, Bayes’ theorem states

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=Pr(Y=k|X=x)=p_k(X)=\displaystyle \frac{\pi_k f_k(X)}{\sum_{j=1}^k\pi_j f_j(X)}">
</p>

where <img src="https://render.githubusercontent.com/render/math?math=\pi_k"> denotes the prior probability that the chosen observation comes from the kth class. This equation is sometimes abbreviated as <img src="https://render.githubusercontent.com/render/math?math=p_k(x)">.


<img src="https://render.githubusercontent.com/render/math?math=p_k(X)=Pr(Y=k|X)"> is also known as the posterior probability, or the probability that an observation belongs to the kth class, given the predictor value for that observation.

Estimating <img src="https://render.githubusercontent.com/render/math?math=\pi_k">, the prior probability, is easy given a random sample of responses from the population.

Estimating the density function, <img src="https://render.githubusercontent.com/render/math?math=f_k(X)"> tends to be harder, but making some assumptions about the form of the densities can simplify things. A good estimate for <img src="https://render.githubusercontent.com/render/math?math=f_k(X)"> allows for developing a classifier that approximates the Bayes’ classifier which has the lowest possible error rate since it always selects the class for which <img src="https://render.githubusercontent.com/render/math?math=p_k(x)">  is largest.

**Linear discriminant analysis for one predictor** we assume that <img src="https://render.githubusercontent.com/render/math?math=f_k(X)"> has a normal distribution, or Gaussian distribution, the normal density is described by


<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=f_k(X) = \frac{1}{2\sqrt{2\pi}\sigma_k} exp[-\frac{1}{2\sigma_k^2}(x - \mu_k)^2]">
</p>

where <img src="https://render.githubusercontent.com/render/math?math=\mu_k"> is the mean parameter for the kth class and <img src="https://render.githubusercontent.com/render/math?math=\sigma_k^2"> is the variable parameter for the kth class.

The density function can be further simplified by assuming that the variance terms, 

<img src="https://render.githubusercontent.com/render/math?math=\sigma_1^2, ..., \sigma_k^2">, are all equal in which case the variance is denoted by <img src="https://render.githubusercontent.com/render/math?math=\sigma_1^2, ..., \sigma^2">.
Plugging the simplified normal density function into Bayes’ theorem yields


<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=p_k(x)= \displaystyle  \frac{\pi_k \frac{1}{\sqrt{2\pi}\sigma} exp[-\frac{1}{2\sigma_k^2}(x - \mu_k)^2]}{\sum_{j=1}^k\pi_j \frac{1}{\sqrt{2\pi}\sigma} exp[-\frac{1}{2\sigma_k^2}(x - \mu_j)^2]}">
</p>

It can be shown that by taking a log of both sides and removing terms that are not class specific, a simpler equation can be extracted:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\delta_{k}(x) = \frac{x\mu_{k}}{\sigma^{2}} - \frac{\mu_{k}^{2}}{2\sigma^{2}}
+ \log(\pi_{k})"> 
</p>

Using this equation, an observation can be classified by taking the class yields the largest value.

Linear discriminant analysis uses the following estimated values for <img src="https://render.githubusercontent.com/render/math?math=\mu^k"> and <img src="https://render.githubusercontent.com/render/math?math=\sigma^2">:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\hat{\mu}_{k} = \frac{1}{n_{k}}\sum_{i:y_{i} = k}x_{i}">
</p>

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\sigma^{2} = \frac{1}{n - k} \displaystyle \sum_{k=1}^{k} \displaystyle \sum_{i:y_{i} = k} (x_{i} - \mu_{k})^{2}">
</p>

where n is the total number of training observations and <img src="https://render.githubusercontent.com/render/math?math=n_k"> is the number of training observations in class k.

The estimate of <img src="https://render.githubusercontent.com/render/math?math=\mu^k"> is the average value of x for all training observations in class k.

The estimate of <img src="https://render.githubusercontent.com/render/math?math=\sigma^2"> can be seen as a weighted average of the sample variance for all k classes.

When the class prior probabilities, <img src="https://render.githubusercontent.com/render/math?math=\pi_1, ... \pi_n">, is not known, it can be estimated using the proportion of training observations that fall into the kth class:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\hat{\pi_k} = \frac{n_k}{n}">
</p>

Plugging the estimates for 
<img src="https://render.githubusercontent.com/render/math?math=\hat{\mu}_k"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{\sigma}_k^2"> into the modified Bayes’ theorem yields the linear discriminant analysis classifer:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\hat{\delta}_{k}(x) = \frac{x\hat\mu_{k}}{\hat\sigma^{2}} - \frac{\hat\mu_{k}^{2}}{2\hat\sigma^{2}} + \log(\hat\pi_{k})"> 
</p>

which assigns an observation X=x to whichever class yields the largest value.

This classifier is described as linear because the discriminant function <img src="https://render.githubusercontent.com/render/math?math=\hat\sigma_k(x)"> is linear in terms of x and not a more complex function.

The Bayes decision boundary for linear discriminant analysis is identified by the boundary where <img src="https://render.githubusercontent.com/render/math?math=\delta_k(x) = \delta_j(x)">.
The linear discriminant analysis classifier assumes that the observations from each class follow a normal distribution with a class specific average vector and constant variance, <img src="https://render.githubusercontent.com/render/math?math=\sigma^2">, and uses these simplifications to build a Bayes’ theorem based classifier.

**Multivariate linear discriminant analysis** assumes that <img src="https://render.githubusercontent.com/render/math?math=X=(X_1, X_2 , ..., X_p)"> comes from a multivariate normal distribution with a class-specific mean vector and a common covariance matrix.

The multivariate Gaussian distribution used by linear discriminant analysis assumes that each predictor follows a one-dimensional normal distribution with some correlation between the predictors. The more correlation between predictors, the more the bell shape of the normal distribution will be distorted.

A p-dimensional variable X can be indicated to have a multivariate Gaussian distribution with the notation <img src="https://render.githubusercontent.com/render/math?math=X ~ N(\mu, \Sigma)">, where <img src="https://render.githubusercontent.com/render/math?math=E(x)=\mu"> is the mean of X (a vector with p components) and <img src="https://render.githubusercontent.com/render/math?math=Cov(X)=\Sigma"> is the p x p covariance matrix of X.

Multivariate Gaussian density is formally defined as:

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\normalsize f(x) = \frac{1}{(2\pi)^{p/2}|\Sigma|^{1/2}} \exp \big \lgroup -\frac{1}{2}(x - \mu)^{T}\Sigma^{-1}(x - \mu) \big \rgroup">
</p>

For linear discriminant analysis with multiple predictors, the multivariate Gaussian distribution, <img src="https://render.githubusercontent.com/render/math?math=N(\mu_k, \Sigma)">, is assumed to have a class specific mean vector, <img src="https://render.githubusercontent.com/render/math?math=\mu_k">, and a covariance vector common to all classes, <img src="https://render.githubusercontent.com/render/math?math=\Sigma">.

Combining the multivariate Gaussian density function with Bayes’ theorem yields the vector/matrix version of the linear discriminant analysis Bayes’ classifier:


<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\normalsize \delta_{k}(x) = x^{T} \Sigma^{-1} \mu_{k} - \frac{1}{2} \mu_{k}^{T}
\Sigma^{-1} \mu_{k} %2B \log \pi_{k}">
</p>
Again, whichever class yields the largest value is the highest probability classification.

The Bayes decision boundaries are defined by the values for which 

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\normalsize x^{T} \Sigma^{-1} \mu_{j} - \frac{1}{2} \mu_{j}^{T} \Sigma^{-1}\mu_{j} =
x^{T} \Sigma^{-1} \mu_{k} - \frac{1}{2} \mu_{k}^{T} \Sigma^{-1} \mu_{k}">
</p>

It should be noted that since all classes are assumed to have the same number of training observations, the 
<img src="https://render.githubusercontent.com/render/math?math=log \pi"> terms cancel out.

As was the case for one-dimensional linear discriminant analysis, it is necessary to estimate the unknown parameters <img src="https://render.githubusercontent.com/render/math?math=\mu_1,..., \mu_k"> and <img src="https://render.githubusercontent.com/render/math?math=\pi_1,..., \pi_k">
and <img src="https://render.githubusercontent.com/render/math?math=\Sigma">. The formulas used in the multi-dimensional case are similar to those used with just a single dimension.

Since, even in the multivariate case, the linear discriminant analysis decision rule relates to X in a linear fashion, the name linear discriminant analysis holds.

As with other methods, the higher the ratio of parameters, p, to number of samples, n, the more likely overfitting will occur.

In general, binary classifiers are subject to two kinds of error: false positives and false negatives. A confusion matrix can be a useful way to display these error rates. Class-specific performance is also important to consider because in some cases a particular class will contain the bulk of the error.

In medicine and biology, the term sensitivity refers to the percentage of observations correctly positively classified (true positives) and specificity refers to the percentage of observations correctly negatively classified (true negatives).

In a two-class scenario, the Bayes classifier, and by extension, linear discriminant analysis, uses a 50% threshold for the posterior probability when determining classifications. In some cases it may be desirable to lower this threshold.

A ROC curve is a useful graphic for displaying the two types of error rates for all possible thresholds. ROC is a historic acronym that comes from communications theory and stands for receiver operating characteristics.

The overall performance of a classifier summarized over all possible thresholds is quantified by the area under the ROC curve.

**Quadratic discriminant analysis** offers an alternative approach to linear discriminant analysis that makes most of the same assumptions, except that quadratic discriminant analysis assumes that each class has its own covariance matrix. This amounts to assuming that an observation from the kth class has a distribution of the form <img src="https://render.githubusercontent.com/render/math?math=X~N(\mu_k, \Sigma_k)"> where <img src="https://render.githubusercontent.com/render/math?math=\Sigma_k"> is a covariance matrix for class k.

This yields a Bayes classifier that assigns an observation X=x to the class with the largest value for

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=\normalsize \delta_{k}(x) = - \frac{1}{2}(x - \mu_{k})^{T} \Sigma_{k}^{-1} (x
- \mu_{k}) - \frac{1}{2} \log |\Sigma_{k}| %2B log \pi_{k}">
</p>

which is equivalent to

<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math=
\normalsize \delta_{k}(x) = - \frac{1}{2}x^{T} \Sigma_{k}^{-1} %2B x^{T}
\Sigma_{k}^{-1}\mu_{k} - \frac{1}{2}\mu_{k}^{T} \Sigma_{k}^{-1} \mu_{k} -
\frac{1}{2} \log | \Sigma_{k} | %2B \log \pi_{k}">
</p>

The quadratic discriminant analysis Bayes classifier gets its name from the fact that it is a quadratic function in terms of x.
The choice between a shared covariance matrix (like that assumed in linear discriminant analysis) and a class-specific covariance matrix (like that assumed in quadratic discriminant analysis) amounts to a bias-variance trade-off. This is because when there are p predictors, estimating a covariance matrix requires estimating <img src="https://render.githubusercontent.com/render/math?math=\frac{p(p+1)}{2}"> parameters. Since quadratic discriminant analysis estimates a separate covariance matrix for each class, this amounts to estimating <img src="https://render.githubusercontent.com/render/math?math=\frac{kp(p+1)}{2}"> parameters.

By assuming a common covariance matrix, linear discriminant analysis is linear in terms of x which means Kp linear coefficients must be estimated. Because of this, linear discriminant analysis is much less flexible than quadratic discriminant analysis, but as a result has much lower variance. If the assumption of a common covariance matrix is highly inaccurate, it can cause linear discriminant analysis to suffer from high bias.

In general terms, linear discriminant analysis tends to be a better choice if the importance of reducing variance is important because there are relatively few training examples. Conversely, quadratic discriminant analysis can be a better choice if the training set is large such that the variance of the classifier is not a concern or if the assumption of a common covariance matrix is not realistic.

**Comparing the models**
Since logistic regression and linear discriminant analysis are both linear in terms of x, the primary difference between the two methods is their fitting procedures. Linear discriminant analysis assumes that observations come from a Gaussian distribution with a common covariance matrix, and as such, out performs logistic regression in cases where these assumptions hold true.

K-nearest neighbors can outperform linear regression and linear discriminant analysis when the decision boundary is highly non-linear, but at the cost of a less interpretable model.

Quadratic discriminant analysis falls somewhere between the linear approaches of linear discriminant analysis and logistic regression and the non-parametric approach of K-nearest neighbors. Since quadratic linear analysis models a quadratic decision boundary, it has more capacity for modeling a wider range of problems.

Quadratic discriminant analysis is not as flexible as K-nearest neighbors, however it can perform better than K-nearest neighbors when there are fewer training observations due to its high bias.

Linear discriminant analysis and logistic regression will perform well when the true decision boundary is linear.

Quadratic discriminant analysis may give better results when the decision boundary is moderately non-linear.

Non-parametric approaches like K-nearest neighbors may give better results when the decision boundary is more complex and the right level of smoothing is employed.

As was the case in the regression setting, it is possible to apply non-linear transformations to the predictors to better accommodate non-linear relationships between the response and the predictors.

The effectiveness of this approach will depend on whether or not the increase in variance introduced by the increase in flexibility is offset by the reduction in bias.

It is possible to add quadratic terms and cross products to the linear discriminant analysis model such that it has the same form as quadratic discriminant analysis, however the parameter estimates for each of the models would be different. In this fashion, it’s possible to build a model that falls somewhere between linear discriminant analysis and quadratic discriminant analysis.

#### Further reading:
* <a href="https://youtu.be/XepXtl9YKwc" target="_blank">Maximum likelihoood clearly explained!</a>
