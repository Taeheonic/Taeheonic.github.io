---
layout: post
title: "Tutorial for Decision Tree and Random Forest"

use_math: true
---

## **Introduction**
Tree-based model is one of the most used machine learning methods today. It is a supervised learning algorithm that can be applied to both classification and regression problems. There are many R or Python packages that automatically make a decision tree with a single line of code. However, this is not a tutorial of how to use such package. Rather, this will guide how to create a tree step by step so that you can understand what is happening in the decision tree and ensemble model. This tutorial is designed for people who don’t have any background about data mining or machine learning, but want to learn what is decision tree, how does decision tree work, and how is it used in ensemble models such as random forest algorithm. This tutorial will use a ‘Acute Inflammation’ dataset from UCI machine learning repository to focus on explaining classification tree and it will also includes little bit of mathematics and coding for better understanding.
___
## **What is decision tree?**
I’m sure you have used a decision tree algorithm in your life. When you want to guess opponent’s quiz game and your opponent can only answer yes or no, you need to ask multiple questions in order to narrow the questions down to the answer (i.e. Twenty Questions Game). You are using a strategy similar to the decision tree algorithm in your head whenever you ask questions to the opponent; you tend to choose the question that splits or partitions best your ideas. Let’s talk about basic terminology before we begin talking about the algorithm.

add img

The graph above is an example of a decision tree using some data. It uses binary predictor variables and classifying binary response variable, so this is an example of classification tree.

V4, V5, and V3 are the predictors of the data and they are nodes of the tree. But, they are not the same nodes. V4 is 	called root node where the data is being split first. V3 and V5 are called decision nodes which are also the place where the data is being split. I’m going to explain how to choose which node to make as a root node and which nodes to make as decision nodes. The nodes that don’t have branch underneath, they are called leaf nodes or terminal nodes.

If you look at the tree, there are 4 leaf nodes. In each node, there are two numbers in each leaf node. For example, the very left leaf node have 40 and 0. This means there are 40 observations that are not V4, and all 40 observations are classified as no and 0 observation is classified as yes. If you add all the numbers in the leaf nodes, it will give the total observations. In this example, there are 120 observations and split three times at V4, V5, and V3 nodes.

As you might already have guessed, all the leaf nodes are classified perfectly (n vs 0 or 0 vs n). It looks like the decision tree is the best machine learning method for classification! However, it is not the case for the real world data. When the leaf node is not 100% classified as one or the other, it is considered as impure or uncertain. Thus, we need to find a way to measure or calculate this impurity so that we can minimize it. The most used method of measuring this impurity is called Gini impurity or Gini index. Here is the formula for the Gini index. There are other methods like cross-entropy or classification error rate, but we are only going to talk about Gini index in this tutorial

$$
*G.I*(A) = \sum_{i=1}^d (R_*i*(1- \sum_{k=1}^m (p_{*ik*}^2)))
$$


___






This formula $f(x) = x^2$ is an example.

$$
\lim_{x\to 0}{\frac{e^x-1}{2x}}
\overset{\left[\frac{0}{0}\right]}{\underset{\mathrm{H}}{=}}
\lim_{x\to 0}{\frac{e^x}{2}}={\frac{1}{2}}
$$


![masi]({{site.baseurl}}/images/masi.jpg)
<img src="{{site.baseurl}}/images/masi.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="msai"><br/>
<img src="{{site.baseurl}}/images/masi.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="masi">