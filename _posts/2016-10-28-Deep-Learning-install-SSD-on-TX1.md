---
layout: post
title:  "Install SSD on Jetson TX1"
categories: Deep-Learning
comments: true
tags:  Deep-Learning SSD TX1 
author: Jaehyek
---

refer to the URL <https://github.com/DrewNF/Build-Deep-Learning-Env-with-Tensorflow-Python-OpenCV>

#### After install the above link, and install the following 

```
sudo apt-get install libatlas-base-dev 
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install libopenblas-dev
```

and add lib to Makefile  like this:
in Makefile
LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial boost_regex

#### install opencv2 

```
sudo apt-get install build-essential cmake git pkg-config
sudo apt-get install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev
sudo apt-get install libgtk2.0-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python2.7-dev

wget https://bootstrap.pypa.io/get-pip.py --no-check-certificate
sudo python get-pip.py 
pip install numpy
```

```
$ cd ~ 
$ git clone https://github.com/daveselinger/opencv
$ cd opencv 
$ git checkout 3.1.0-with-cuda8
```

```
$ cd ~ 
$ git clone https://github.com/Itseez/opencv_contrib.git 
$ cd opencv_contrib 
$ git checkout 3.1.0
```

