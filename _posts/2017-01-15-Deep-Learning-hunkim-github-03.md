---
layout: post
title:  "Deep Learning summary from http://hunkim.github.io/ml/ (3)"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---

# Convolutional Neural Networks

#### refer to http://cs231n.stanford.edu/

1. Let’s focus on a small area only (5x5x3) 

![001](/img/2017-01-15-Deep-Learning-hunkim-github-03/001.JPG)

2. Get one number using the filter

![002](/img/2017-01-15-Deep-Learning-hunkim-github-03/002.JPG)

3. Let’s look at other areas with the same filter (w)

![003](/img/2017-01-15-Deep-Learning-hunkim-github-03/003.JPG)


4. In practice: Common to zero pad the border

![004](/img/2017-01-15-Deep-Learning-hunkim-github-03/004.JPG)


5. Swiping the entire image

![005](/img/2017-01-15-Deep-Learning-hunkim-github-03/005.JPG)

6. Convolution layers

![006](/img/2017-01-15-Deep-Learning-hunkim-github-03/006.JPG)
![007](/img/2017-01-15-Deep-Learning-hunkim-github-03/007.JPG)

7. Pooling layer (sampling) & MAX POOLING

![008](/img/2017-01-15-Deep-Learning-hunkim-github-03/008.JPG)
![009](/img/2017-01-15-Deep-Learning-hunkim-github-03/009.JPG)

8. Fully Connected Layer (FC layer)
Contains neurons that connect to the entire input volume, as in ordinary Neural Networks

![010](/img/2017-01-15-Deep-Learning-hunkim-github-03/010.JPG)

9. ConvNetJS demo: training on CIFAR-10]

refer to <http://cs.stanford.edu/people/karpathy/convnetjs/demo/cifar10.html>


# CNN Case Study

#### Case Study: LeNet-5 [LeCun et al., 1998]

#### Case Study: AlexNet [Krizhevsky et al. 2012]

#### Case Study: GoogLeNet [Szegedy et al., 2014]

#### Case Study: ResNet [He et al., 2015]

- Slide from Kaiming He’s recent presentation https://www.youtube.com/watch?v=1PGLj-uKT1w
- ILSVRC 2015 winner (3.6% top 5 error)
- 2-3 weeks of training on 8 GPU machine
- at runtime: faster than a VGGNet! (even though it has 8x more layers)


![011](/img/2017-01-15-Deep-Learning-hunkim-github-03/011.JPG)
![012](/img/2017-01-15-Deep-Learning-hunkim-github-03/012.JPG)
![013](/img/2017-01-15-Deep-Learning-hunkim-github-03/013.JPG)
![014](/img/2017-01-15-Deep-Learning-hunkim-github-03/014.JPG)

