---
layout: post
title: "Tutorial for Decision Tree and Random Forest"

use_math: true
---

## **Introduction**
Tree-based model is one of the most used machine learning methods today. It is a supervised learning algorithm that can be applied to both classification and regression problems. There are many R or Python packages that automatically make a decision tree with a single line of code. However, this is not a tutorial of how to use such package. Rather, this will guide how to create a tree step by step so that you can understand what is happening in the decision tree and ensemble model. This tutorial is designed for people who don’t have any background about data mining or machine learning, but want to learn what is decision tree, how does decision tree work, and how is it used in ensemble models such as random forest algorithm. This tutorial will use a ‘Acute Inflammation’ dataset from UCI machine learning repository to focus on explaining classification tree and it will also includes little bit of mathematics and coding for better understanding.


This formula $f(x) = x^2$ is an example.

$$
\lim_{x\to 0}{\frac{e^x-1}{2x}}
\overset{\left[\frac{0}{0}\right]}{\underset{\mathrm{H}}{=}}
\lim_{x\to 0}{\frac{e^x}{2}}={\frac{1}{2}}
$$


![masi]({{site.baseurl}}/images/masi.jpg)
<img src="{{site.baseurl}}/images/masi.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="msai"></img><br/>
<img src="{{site.baseurl}}/images/masi.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="masi"></img>