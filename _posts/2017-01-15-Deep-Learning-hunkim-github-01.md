---
layout: post
title:  "Deep Learning summary from http://hunkim.github.io/ml/ (1)"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---

## Simplified Hypothesis and Cost
![001](/img/2017-01-15-Deep-Learning-hunkim-github-01/001.JPG)

#### Gradient descent algorithm
- Minimize cost function
- Gradient descent is used many minimization problems
- For a given cost function, cost (W, b), it will find W, b to minimize cost
- It can be applied to more general function: cost (w1, w2, …)

#### How to work
- Formal definition

![002](/img/2017-01-15-Deep-Learning-hunkim-github-01/002.JPG)
![003](/img/2017-01-15-Deep-Learning-hunkim-github-01/003.JPG)
![004](/img/2017-01-15-Deep-Learning-hunkim-github-01/004.JPG)
![005](/img/2017-01-15-Deep-Learning-hunkim-github-01/005.JPG)

#### Hypothesis with Matrix
![006](/img/2017-01-15-Deep-Learning-hunkim-github-01/006.JPG)

## Logistic (regression) classification

#### Logistic Hypothesis
![007](/img/2017-01-15-Deep-Learning-hunkim-github-01/007.JPG)

#### New cost function for logistic
![008](/img/2017-01-15-Deep-Learning-hunkim-github-01/008.JPG)
![009](/img/2017-01-15-Deep-Learning-hunkim-github-01/009.JPG)

**sample code**

```
h = tf.matmul(W, X)
hypothesis = tf.div(1., 1. + tf.exp(-h))

cost = -tf.reduce_mean(Y * tf.log(hypothesis) + (1 - Y) * tf.log(1 - hypothesis))

a = tf.Variable(0.1)  # learning rate, alpha
optimizer = tf.train.GradientDescentOptimizer(a)
train = optimizer.minimize(cost)  # goal is minimize cost
```

#### Multinomial classification and Where is sigmoid?
![010](/img/2017-01-15-Deep-Learning-hunkim-github-01/010.JPG)

#### SOFTMAX
![011](/img/2017-01-15-Deep-Learning-hunkim-github-01/011.JPG)

#### Cross-entropy cost function
![012](/img/2017-01-15-Deep-Learning-hunkim-github-01/012.JPG)
![013](/img/2017-01-15-Deep-Learning-hunkim-github-01/013.JPG)
![014](/img/2017-01-15-Deep-Learning-hunkim-github-01/014.JPG)
![015](/img/2017-01-15-Deep-Learning-hunkim-github-01/015.JPG)

#### Data (X) preprocessing for gradient descent
![016](/img/2017-01-15-Deep-Learning-hunkim-github-01/016.JPG)

#### standardization
![017](/img/2017-01-15-Deep-Learning-hunkim-github-01/017.JPG)

- X_std[:,0] = (X[:,0] - X[:,0].mean()) / X[:,0].std()

#### Training, validation and test sets
![018](/img/2017-01-15-Deep-Learning-hunkim-github-01/018.JPG)

#### MINIST Dataset
![019](/img/2017-01-15-Deep-Learning-hunkim-github-01/019.JPG)

- train-images-idx3-ubyte.gz : training set images (9912422 bytes)
- train-labels-idx1-ubyte.gz : training set lables (18881 bytes)

- t10k-images-idx3-ubyte.gz : test set images (1648877 bytes)
- t10k-labels-idx1-ubyte.gz : test set lables ( 4542 bytes)

- <http://yann.lecun.com/exdb/mnist/>

