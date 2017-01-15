---
layout: post
title:  "Deep Learning summary from http://hunkim.github.io/ml/ (2)"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---

#### Canadian Institute for Advanced Research (CIFAR)

#### Google DeepMind's Deep Q-learning playing Atari Breakout
![001](/img/2017-01-15-Deep-Learning-hunkim-github-02/001.JPG)
<https://youtu.be/V1eYniJ0Rnk>

#### Multinomial classification
![002](/img/2017-01-15-Deep-Learning-hunkim-github-02/002.JPG)

#### Back propagation
![003](/img/2017-01-15-Deep-Learning-hunkim-github-02/003.JPG)

### 5 steps of using tensorboard
1. From TF graph, decide which node you want to annotate
 - with tf.name_scope("test") as scope:
 - tf.histogram_summary("weights", W), tf.scalar_summary(“accuracy", accuracy)

2. Merge all summaries
 - merged = tf.merge_all_summaries()
 
3. Create writer
 - writer = tf.train.SummaryWriter("/tmp/mnist_logs", sess.graph_def)
 
4. Run summary merge and add_summary
 - summary = sess.run(merged, …); writer.add_summary(summary);
 
5. Launch Tensorboard
 - tensorboard --logdir=/tmp/mnist_logs
 - You can navigate to http://0.0.0.0:6006

![004](/img/2017-01-15-Deep-Learning-hunkim-github-02/004.JPG)

```
import tensorflow as tf
import numpy as np

xy = np.loadtxt('07train.txt', unpack=True)
x_data = np.transpose(xy[0:-1])
y_data = np.reshape(xy[-1], (4, 1))

print x_data
print y_data

X = tf.placeholder(tf.float32, name='x-input')
Y = tf.placeholder(tf.float32, name='y-input')

w1 = tf.Variable(tf.random_uniform([2, 5], -1.0, 1.0), name='weight1')
w2 = tf.Variable(tf.random_uniform([5, 10], -1.0, 1.0), name='weight2')
w3 = tf.Variable(tf.random_uniform([10, 10], -1.0, 1.0), name='weight3')
w4 = tf.Variable(tf.random_uniform([10, 10], -1.0, 1.0), name='weight4')
w5 = tf.Variable(tf.random_uniform([10, 10], -1.0, 1.0), name='weight5')
w6 = tf.Variable(tf.random_uniform([10, 10], -1.0, 1.0), name='weight6')
w7 = tf.Variable(tf.random_uniform([10, 10], -1.0, 1.0), name='weight7')
w8 = tf.Variable(tf.random_uniform([10, 1], -1.0, 1.0), name='weight8')

b1 = tf.Variable(tf.zeros([5]), name="Bias1")
b3 = tf.Variable(tf.zeros([10]), name="Bias3")
b2 = tf.Variable(tf.zeros([10]), name="Bias2")
b4 = tf.Variable(tf.zeros([10]), name="Bias4")
b5 = tf.Variable(tf.zeros([10]), name="Bias5")
b6 = tf.Variable(tf.zeros([10]), name="Bias6")
b7 = tf.Variable(tf.zeros([10]), name="Bias7")
b8 = tf.Variable(tf.zeros([1]), name="Bias8")

L2 = tf.nn.relu(tf.matmul(X, w1) + b1)
L3 = tf.nn.relu(tf.matmul(L2, w2) + b2)
L4 = tf.nn.relu(tf.matmul(L3, w3) + b3)
L5 = tf.nn.relu(tf.matmul(L4, w4) + b4)
L6 = tf.nn.relu(tf.matmul(L5, w5) + b5)
L7 = tf.nn.relu(tf.matmul(L6, w6) + b6)
L8 = tf.nn.relu(tf.matmul(L7, w7) + b7)

hypothesis = tf.sigmoid(tf.matmul(L8, w8) + b8)

with tf.name_scope('cost') as scope:
    cost = -tf.reduce_mean(Y * tf.log(hypothesis) + (1-Y) * tf.log(1 - hypothesis))
    cost_summ = tf.summary.scalar("cost", cost)

with tf.name_scope('train') as scope:
    a = tf.Variable(0.1)
    optimizer = tf.train.GradientDescentOptimizer(a)
    train = optimizer.minimize(cost)

w1_hist = tf.summary.histogram("weights1", w1)
w2_hist = tf.summary.histogram("weights2", w2)

b1_hist = tf.summary.histogram("biases1", b1)
b2_hist = tf.summary.histogram("biases2", b2)

y_hist = tf.summary.histogram("y", Y)

init = tf.global_variables_initializer()

with tf.Session() as sess:
    sess.run(init)

    merged = tf.summary.merge_all()
    writer = tf.summary.FileWriter("./logs/xor_logs", sess.graph)

    for step in xrange(20000):
        sess.run(train, feed_dict={X: x_data, Y: y_data})
        if step % 200 == 0:
            summary = sess.run(merged, feed_dict={X: x_data, Y: y_data})
            writer.add_summary(summary, step)
            print step, sess.run(cost, feed_dict={X: x_data, Y: y_data}), sess.run(w1), sess.run(w2)

    correct_prediction = tf.equal(tf.floor(hypothesis+0.5), Y)

    accuracy = tf.reduce_mean(tf.cast(correct_prediction, "float"))
    print sess.run([hypothesis, tf.floor(hypothesis+0.5), correct_prediction], feed_dict={X: x_data, Y: y_data})
    print "accuracy", accuracy.eval({X: x_data, Y: y_data})
```
 
 
#### ReLU: Rectified Linear Unit
- L1 = tf.sigmoid(tf.matmul(X, W1) + b1)
- L1 = tf.nn.relu(tf.matmul(X, W1) + b1)

- maxout = max(w1x + b1, w2x + b2 ) 

#### Activation functions on CIFAR-10
![005](/img/2017-01-15-Deep-Learning-hunkim-github-02/005.JPG)

#### Need to set the initial weight values wisely
- Not all 0’s
- Challenging issue
- Hinton et al. (2006) "A Fast Learning Algorithm for Deep Belief Nets”
 - Restricted Boatman Machine (RBM)
 
