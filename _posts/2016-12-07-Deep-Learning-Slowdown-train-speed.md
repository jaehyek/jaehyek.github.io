---
layout: post
title:  "Causes of learning slowdown phenomenon"
categories: Deep-Learning
comments: true
tags:  Deep-Learning  Machine-Learning slowdown
author: Jaehyek
---

refer to <http://laonple.blog.me/220548474619>

#### Problem of Neural Network Learning Speed - Learning Slowdown

If the difference between the original value (the result of the training data) and the actual value of network is large, Will the learning really work ? <br/>
Generally the  method of MSE ( Mean Square Error )  to use the cost function of neural network doesn't work well unfontunately '

Why? <br/>
in case that you use the cost function as MSE and Sigmoid as active function, it is because that a problem is assoicated with Sigmoid characteristics

**Cause of learning slowdown of neural network -- due to the differential nature of sigmoid function** <br/>
 To explain easily let's guess that we have one neuron, w weight, b bias and active function as sigmoid  like as the below picture <br/>

When a input is x, the input of neuron is z = wx + b <br/>
passing the active function σ(z), the output a comes out.

![001](/img/2016-12-07-Deep-Learning-Slowdown-train-speed/001.JPG)

if the output is y when a input is x , <br/>
the cost function is the red box like as above picture.

Here (y – a) is error , and make the error back-propagate. and then <br/>
The larger the error , the faster the learning  should be.  

As we inspected with back-propagation page, <br/>
To update the value of weight and bias  the cost function C performs partial-differential for weight and bias. 
After performing the partial-differential, the result as the below red box comes out.

![002](/img/2016-12-07-Deep-Learning-Slowdown-train-speed/002.JPG)

As you can see from the above equation, <br/>
the partial differential value of weight and bias have the multiplication with sigmoid derivative. <br/>
Right this is a main curprit.

When we have the derivative for sigmoid function, the result like as the above picture comes out.<br/>
That is, z equal to 0 , then get the maximum, and the farther from 0, the smaller to 0  the derivative value goes. <br/>
That is, the updated value of weight and bias has a form to multiply the very small value, <br/>
and then although (a-y) item is very large, finally the z value would become a very small value, and make the learning speed slowdown. 

**Cause of learning slowdown of neural network -- due to the gradient decent nature** <br/>

When  we see the partial differential equation of C/W, <br/>
the value of (a - y ) becomes small, that is, the target value and the  real value of network become almost same , <br/>
the value of (a - y ) becomes again close to 0, and finally the updated value of weight and bias become smaller. <br/>
finally when goes close to 0, and the learning speed become slowdown.
 
This is due to the structural characteristics of the gradient descent method. <br/>
As we saw earlier in "class 8", the gradient descent method is the result.

![003](/img/2016-12-07-Deep-Learning-Slowdown-train-speed/003.JPG)
 
When you drop the ball from a high place, <br/>
No matter where you start, <br/>
The larger the gradient (the larger the gradient), the faster it moves. <br/>
Then when it comes to the bottom (ie near the target) <br/>
Because there is little slope, the speed at which the ball rolls is slowed down.

Finally when (a - y ) goes close to 0,
the learning speed become slow, <br/>
a phenomenon occurs in which the result of learning does not improve so much even if the learning is further performed.


**Cross-Entropy**
The cross-entropy cost function is defined as follows. <br/>
Where y is the expected value, <br/>
Assuming that a is a value output from the actual network, <br/>
Let n be the number of training data.

![004](/img/2016-12-07-Deep-Learning-Slowdown-train-speed/004.JPG)

Using the sigmoid function as an active function

![005](/img/2016-12-07-Deep-Learning-Slowdown-train-speed/005.JPG)

As we initially expected, we were able to get results that were proportional to the difference between expected and actual output.<br/>
As a result, when the learning is performed using the CE cost function, <br/>
Because learning progresses much faster <br/>
Nowadays, we use CE cost function more than MSE

