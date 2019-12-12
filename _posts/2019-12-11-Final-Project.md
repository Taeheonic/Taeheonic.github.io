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

![tree1]({{site.baseurl}}/images/tree1.jpg)

The graph above is an example of a decision tree using some data. It uses binary predictor variables and binary response variable, so this is an example of classification tree.

V4, V5, and V3 are the predictors of the data and they are nodes of the tree. But, they are not the same nodes. V4 is 	called root node where the data is being split first. V3 and V5 are called decision nodes which are also the place where the data is being split. I’m going to explain how to choose which node to make as a root node and which nodes to make as decision nodes later in this tutorial. The nodes that don’t have branch underneath, they are called leaf nodes or terminal nodes.

If you look at the tree, there are 4 leaf nodes. In each node, there are two numbers in each leaf node. For example, the very left leaf node have 40 and 0. This means there are 40 observations that are not V4, and all 40 observations are classified as no and 0 observation is classified as yes. If you add all the numbers in the leaf nodes, it will give the total observations. In this example, there are 120 observations and split three times at V4, V5, and V3 nodes.

As you might already have guessed, all the leaf nodes are classified perfectly (n vs 0 or 0 vs n). It looks like the decision tree is the best machine learning method for classification! However, it is not the case for the real world data. When the leaf node is not 100% classified as one or the other, it is considered as impure or uncertain. Thus, we need to find a way to measure or calculate this impurity so that we can minimize it. The most used method of measuring this impurity is called Gini impurity or Gini index. Here is the formula for the Gini index. There are other methods like cross-entropy or classification error rate, but I am only going to talk about Gini index in this tutorial.

$$
G.I(A) = \sum_{i=1}^d (R_i(1- \sum_{k=1}^m (p_{ik}^2))) \\
Entropy(A) = -\sum_{k=1}^m (p_k) log(p_k)
$$

___

It is time to actually make a decision tree step by step. I will use a subset of ‘Acute Inflammation’ dataset in order to make an example simple. It has 3 predictors (Lumbar pain, Urine pushing, and Micturition pains) and 1 response variable (Decision). All 4 variables are binary data.

First step of making a decision tree is a choosing root node. As I mentioned earlier, I will use Gini impurity as a method of measurement. The table below is a sample of the data I am going to  use.

<img src="{{site.baseurl}}/images/table1.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="table1">

Let’s consider only Lumbar pain predictor and Decision on disease diagnosis (Nephritis or renal pelvis origin) response variable. Because both variables are binary, you can easily classify them. Suppose that you are making a small tree with one predictor and one response variable.

![tree2]({{site.baseurl}}/images/tree2.jpg)

It will look like as a figure above. 50 patients don’t have Lumbar pain and 70 patients have Lumbar pain. The left leaf node shows that 50 patients are diagnosed as having no disease and 0 patients are diagnosed as disease. The impurity of left node is measured as following:

$$
1 -({\frac{\text{disease no}}{total}})^2 -({\frac{\text{disease yes}}{total}})^2 \\
1 -({\frac{50}{50}})^2 -({\frac{0}{50}})^2 = 0
$$

The right leaf node shows that 20 patients are diagnosed as having no disease and 50 patients are diagnosed as disease. The impurity of right node is measured exactly the same as the left node.

$$
1 -({\frac{20}{20+50}})^2 -({\frac{50}{20+50}})^2 = 0.4081633
$$

After calculating both left and right leaf nodes’ impurities, the impurity of Lumbar pain can be measured by using weighted average. The formula for weighted average is:

$$
(\frac{\text{# of patients in left leaf}}{total})*\text{impurity of left leaf} + (\frac{\text{# of patients in right leaf}}{total})*\text{impurity of right leaf} \\
(\frac{50}{120})*0 + (\frac{70}{120})*0.4081633 = 0.2380953
$$

Finally, you got the Gini impurity for Lumbar pain predictor. You need to do the same steps for Urine push and Micturition pain predictors.

$$
\text{Urine push Impurity left} = 1 - (\frac{30}{40})^2 - (\frac{10}{40})^2 = 0.375 \\
\text{Urine push Impurity right} = 1 - (\frac{40}{40+40})^2 - (\frac{40}{40+40})^2 = 0.5 \\
\text{Urine push Impurity} = (\frac{40}{120})*0.375 + (\frac{80}{120})*0.5 = 0.458333 \\
\\
\text{Micturition pain Impurity left} = 1 - (\frac{40}{21+40})^2 - (\frac{21}{21+40})^2 = 0.4514915 \\
\text{Micturition pain Impurity right} = 1 - (\frac{30}{29+30})^2 - (\frac{29}{29+30})^2 = 0.4998564 \\
\text{Micturition pain Impurity} = (\frac{61}{120})*0.4514915 + (\frac{59}{120})*0.4998564 = 0.4752709 \\
$$

Now you got all three impurities.

$$
\text{Lumbar pain} = 0.2380953 \\
\text{Urine push} = 0.458333 \\
\text{Micturition pain} = 0.4752709
$$

In order to compare these values, you just need to choose the one with the minimum impurity. In this case, Lumbar pain has the smallest impurity. Thus the root node will become Lumbar pain. The tree that I got so far looks like the one I showed in the above.

![tree2]({{site.baseurl}}/images/tree2.jpg)

Next step is to find which predictor becomes a decision node. The left leaf node is classified as no disease 100%, which means it is not impure and no need to split more. I’m going to use the right leaf node (70 patients) to split. Using right leaf node as a root node, I will do the same steps from the beginning but without the Lumbar pain.

$$
\text{Urine push Impurity left} = 1 - (\frac{20}{10+20})^2 - (\frac{10}{10+20})^2 = 0.44444 \\
\text{Urine push Impurity right} = 1 - (\frac{0}{40})^2 - (\frac{40}{40})^2 = 0 \\
\text{Urine push Impurity} = (\frac{30}{70})*0.44444 + (\frac{40}{70})*0 = 0.1904762 \\ \\
\\
\text{Micturition pain Impurity left} = 1 - (\frac{20}{21+20})^2 - (\frac{21}{21+20})^2 = 0.4977026 \\
\text{Micturition pain Impurity right} = 1 - (\frac{0}{29})^2 - (\frac{29}{29})^2 = 0 \\
\text{Micturition pain Impurity} = (\frac{41}{70})*0.4977026 + (\frac{29}{70})*0 = 0.2926829 \\
$$

Again, I got the impurities for predictors.

$$
\text{Urine push} = 0.1904762 \\
\text{Micturition pain} = 0.2926829
$$

Since Urine push predictor has the lowest impurity, I’ll use it as a decision node. The tree will look like this after adding Urine push:

![tree3]({{site.baseurl}}/images/tree3.jpg)

The right leaf node of Urine push is well classified, so I’m going to use the leaf node for the next data split. The tree will be completed after putting Micturition pain as the last node as a decision tree:

![tree4]({{site.baseurl}}/images/tree4.jpg)
___


![masi]({{site.baseurl}}/images/masi.jpg)
<img src="{{site.baseurl}}/images/masi.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="msai"><br/>
<img src="{{site.baseurl}}/images/masi.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="masi">