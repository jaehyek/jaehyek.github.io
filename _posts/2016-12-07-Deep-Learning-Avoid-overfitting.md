---
layout: post
title:  "Avoid Overfitting"
categories: Deep-Learning
comments: true
tags:  Deep-Learning  Machine-Learning overfitting
author: Jaehyek
---

#### What is the overfitting 

![001](/img/2016-12-07-Deep-Learning-Avoid-overfitting/001.JPG)
Let's look over the above picture. Given some blue points, guess a curve to represent the points 

- picture(a) : seems like that a simple line has a error to represent those.
- picture(c) : is inferenced that the lime represent the whole points perfectly. but Although it got the optimization results, if  given a point,
 that would produce the wrong result.  we call this overfitting !!!.
- picture(b) : the line represents the whole points although it has a little error. also if given a point , it would still represent the whole thing well.

#### How to resolve the overfitting ? 

The perfect solution to avoid the overfitting is to collect a lot of data.
But it would make a lot of time or cost.  sometime it would be difficult or impossible to gathering more data. 

Additinally if given a lot of  training data,  increasing training time would also become a issue.

When statistical inferencing or running the machime learning normally, the cost function or error function goes to a lower error. 
But just simple lower error can go to bad result.

the below picture showes that the regularization makes good results.
 
![002](/img/2016-12-07-Deep-Learning-Avoid-overfitting/002.JPG)

*** the mathematical presentation of Regularization** .

![003](/img/2016-12-07-Deep-Learning-Avoid-overfitting/003.JPG)

C0 = Cost function
n = data count 
λ = traning rate 
w = weights

the learning direction is to go the lower cost , and also the w value got to go to lower
 
By Differentiating with w , finally a new w get to become like below .  

![004](/img/2016-12-07-Deep-Learning-Avoid-overfitting/004.JPG)

At the above, (1 – ηλ/n)w will make the w value lower  as the n increases. <br/>
This is called "weight decay".
