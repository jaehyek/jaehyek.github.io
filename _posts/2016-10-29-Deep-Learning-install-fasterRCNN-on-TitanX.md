---
layout: post
title:  "Install Faster R-CNN on TitanX"
categories: Deep-Learning
comments: true
tags:  Deep-Learning Faster-R-CNN TitanX
author: Jaehyek
---
To install the faster R-CNN on TitanX <br/>
refer to the URL <https://github.com/smallcorgi/Faster-RCNN_TF>

and do the following 

```
pip install matplotlib.pyplot
pip install scipy
apt-get install python-tk 
In tensorflow0.12, I just modified @tf.RegisterShape("RoiPool") to @ops.RegisterShape("RoiPool"), and it worked for me. Maybe you could try it.
pip install pyyaml
```

#### To run demo.

First, download VGGnet_fast_rcnn_iter_70000.ckpt, and then 

```
~/FNRCC/tools $) python /demo.py --model ./VGGnet_fast_rcnn_iter_70000.ckpt
```
