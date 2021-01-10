---
layout: post
title: "Machine Learning: trees bagging and boosting"
date: 2020-10-22
tags: [machinelearning]
---

# Tree-based models

> Tree-based methods partition the feature space into a set of rectangles, and then fit a simple model (like a constant) in each one.
>
> A key advantage of the recursive binary tree is its interpretability.

## regression trees

### Definition

![regtree](/assets/img/2020-10-22/regtree1.png){:class="img-responsive"}

### Estimates

If the partiions of regions are known/fixed

![regtree](/assets/img/2020-10-22/regtree2.png){:class="img-responsive"}

> However finding the best binary partition in terms of minimum sum of squares is generally computationally infeasible.

### Greedy algorithm

![regtree](/assets/img/2020-10-22/treegreedy.png){:class="img-responsive"}

### Stopping and pruning

> Clearly a very large tree might overfit the data, while a small tree might not capture the important structure. Tree size is a tuning parameter governing the model’s complexity, and the optimal tree size should be adaptively chosen from the data.

> One approach would be to split tree nodes only if the decrease in sum-of-squares due to the split exceeds some threshold. This strategy is too short-sighted, however, since a seemingly worthless split might lead to a very good split below it.

> The preferred strategy is to grow a large tree T0 , stopping the splitting process only when some minimum node size (say 5) is reached. Then this large tree is pruned using cost-complexity pruning, which we now describe.

![regtree](/assets/img/2020-10-22/pruning.png){:class="img-responsive"}

![regtree](/assets/img/2020-10-22/pruning2.png){:class="img-responsive"}

[link](https://scikit-learn.org/stable/modules/tree.html#minimal-cost-complexity-pruning)

> The node that achieves the equality at the smallest α is called the weakest link. It is possible that several nodes achieve equality at the same time, and hence there are several weakest link nodes. If there are several nodes that simultaneously achieve the minimum effective, we remove the branch grown out of each of these nodes. 

[link](https://online.stat.psu.edu/stat508/lesson/11/11.8/11.8.2)


## classification trees

![clftree](/assets/img/2020-10-22/classificationtree.png){:class="img-responsive"}

Misclassification error is the one-hot prediction error rate, gini index is the error rate of predicted probability; cross entropy error is the essentially the entropy of phat, which is a measure of uncertainty(impurity).

## issues

### categorical predictors
![categorical](/assets/img/2020-10-22/categorical_predictors.png){:class="img-responsive"}

### missing values
impute, a missing category, surrogate variables

### loss matrix

Gini index with a loss matrix: weight the corresponding terms in the gini index by the element in loss matrix; but this won't work for binary case, since it's simply adding a factor to the gini index; for binary case, observation weighting is used. But observation weighting only works for multiclass if the terms in the same row of loss matrix is the same.(otherwise you don't know which one to use to weight a certain class).

Observation weighting can be used with the deviance as well. The effect of observation weighting is to alter the prior probability on the classes.

class weight in sklearn: When deciding on a split at a node, the algorithm basically calculates some metric (entropy or gini impurity) for the given node and for the two resulting left and right nodes after the split. Comparing them tells you how much the split would improve the result.

The statistics for the child nodes are weighted by the number of samples in the left and right node, respectively.

When you use sample_weight this adjusts the count and replaces it with the sum of the sample weights. class_weight gives equal sample weights for each sample based on its class according to its class proportion.


### binary splits
multiway splits fragment the data too quickly, leaving insufficient data at the next level down; Since multiway splits can be achieved by a series of binary splits, the latter are preferred.

### Other Tree-Building Procedures
ID3 and its later versions, C4.5 and C5.0 were limited to categorical predictors, and used a top-down rule with no pruning. After a tree is grown, the splitting rules that define the terminal nodes can sometimes be simplified: that is, one or more condition
can be dropped without changing the subset of observations that fall in the node. We end up with a simplified set of rules defining each terminal node; these no longer follow a tree structure, but their simplicity might make them more attractive to the user.

### Linear Combination Splits
improved predictive power, lost interpretebility; difficult to optimize.

### Instability of Trees
The major reason for this instability is the hierarchical nature of the process: the effect of an error in the top split is propagated down to all of the splits below it.

### Lack of Smoothness

### Difficulty in Capturing Additive Structure

## MARS: Multivariate Adaptive Regression Splines

It can be viewed as a generalization of stepwise linear regression or a modification of the CART method to improve the latter’s performance in the regression setting.

![mars](/assets/img/2020-10-22/mars1.png){:class="img-responsive"}

![mars](/assets/img/2020-10-22/mars2.png){:class="img-responsive"}

# Bagging

The average of the predictions over a collection of bootstrap samples can reduce variance. This average is a Monte Carlo estimate of the "true" bagging estimates.

![bagging](/assets/img/2020-10-22/bagging1.png){:class="img-responsive"}

[link](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)


<!-- ## Generalized Additive Models

* regression

![gam](/assets/img/2020-10-22/gam1.png){:class="img-responsive"}

* binary classification

![gam](/assets/img/2020-10-22/gam2.png){:class="img-responsive"}

* general

![gam](/assets/img/2020-10-22/gam3.png){:class="img-responsive"}

[link](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)

* fitting additive models

> We fit each function using a scatterplot smoother (e.g., a
cubic smoothing spline or kernel smoother), and provide an algorithm for simultaneously estimating all p functions -->


# Boosting

## AdaBoost.M1

> A weak classifier is one whose error rate is only slightly better than random guessing. The purpose of boosting is to sequentially apply the weak classification algorithm to repeatedly modified versions of the data, thereby producing a sequence of weak classifiers. The predictions from all of them are then combined through a weighted majority vote to produce the final prediction.

## Boosting Fits an Additive Model
Boosting is a way of fitting an additive expansion in a set of elementary “basis” functions.

![boosting](/assets/img/2020-10-22/boosting1.png){:class="img-responsive"}

## Forward Stagewise Additive Modeling

AdaBoost.M1 minimizes the exponential loss criterion via a forward-stagewise additive modeling approach

## Why Exponential Loss?

The principal attraction of exponential loss in the context of additive modeling is computational; it leads to the simple modular reweighting AdaBoost algorithm.

The additive expansion produced by AdaBoost is estimating one-
half the log-odds of P (Y = 1|x). This justifies using its sign as the classification rule in Adaboost M1.

![boosting](/assets/img/2020-10-22/boosting2.png){:class="img-responsive"}

![boosting](/assets/img/2020-10-22/boosting3.png){:class="img-responsive"}

While E entails expectation over the joint distribution of y and x, it's sufficient to minimize the criterion conditional on x.

Both the exponential and deviance loss can be viewed as monotone continuous approximations to misclassification loss. They continuously penalize increasingly negative margin values more heavily than they reward increasingly positive ones. The difference between them is in degree. The penalty associated with binomial deviance increases linearly for large increasingly negative margin, whereas the exponential criterion increases the influence of such observations exponentially.

Squared-error loss is not a good surrogate for misclassification error. For margin values y i f (x i ) > 1 it increases quadratically, thereby placing increasing influence (error) on observations that are correctly classified with increasing certainty, thereby reducing the relative influence of those incorrectly classified y i f (x i ) < 0. Thus, if class assignment is the goal, a monotone decreasing criterion serves as a better surrogate loss function.


In the regression setting, analogous to the relationship between exponential loss and binomial log-likelihood is the relationship between squared-error loss and absolute loss. The population solutions are mean and median respectively. Squared error is less robust. Alternatives include Huber loss.

These considerations suggest than when robustness is a concern, as is especially the case in data mining applications, squared-
error loss for regression and exponential loss for classification are not the best criteria from a statistical perspective. However, they both lead to the elegant modular boosting algorithms in the context of forward stagewise additive modeling. For squared-error loss one simply fits the base learner to the residuals from the current model; exponential loss one performs a weighted fit of the base learner to the output values with weights


## off the shelf procedure
> Some advantages of trees that are sacrificed by boosting are speed, interpretability, and, for AdaBoost, robustness against
overlapping class distributions and especially mislabeling of the training data. A gradient boosted model (GBM) is a generalization of tree boosting that attempts to mitigate these problems, so as to produce an accurate and effective off-the-shelf procedure for data mining.