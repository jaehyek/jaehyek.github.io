---
layout: post
title:  "Install SSD on Jetson TX1"
categories: Deep-Learning
comments: true
tags:  Deep-Learning SSD TX1 
author: Jaehyek
---

refer to the URL <https://myurasov.github.io/2016/11/27/ssd-tx1.html>

#### Before install the above link, and install the following 

```
sudo apt-get install libatlas-base-dev 
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install libopenblas-dev
```
#### Modify the Makefile.config

```
OPENCV_VERSION := 3
CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \
             -gencode arch=compute_20,code=sm_21 \
             -gencode arch=compute_30,code=sm_30 \
             -gencode arch=compute_35,code=sm_35 \
             -gencode arch=compute_50,code=sm_50 \
             -gencode arch=compute_52,code=sm_52 \
             -gencode arch=compute_52,code=sm_53 \ ( 53 추가 )
             -gencode arch=compute_61,code=sm_61

PYTHON_LIB := /usr/lib/x86_64-linux-gnu ( intel CPU Desktop )
PYTHON_LIB := /usr/lib/aarch64-linux-gnu ( Arm CPU Desktop )

INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib
             
```

#### Modify the Makefile
and add lib to Makefile  like this:
in Makefile
LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial boost_regex

#### mount smbfs 

```
sudo mount -t cifs //172.21.26.47/titanx-home/TX1/share  /home/ubuntu/opencv/build2 -o username=ysc,password=lge123
```

#### install opencv2 ( Arm CPU Desktop )

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

만일 "Deep-Learning-install-OpenCV.md"을 이용해서 opencv을 compile시킬 때, 다음과 같은 error가 나온다. 
```
/home/epinux/dev/opencv_contrib/modules/tracking/include/opencv2/tracking/onlineMIL.hpp:57:23: error: expected unqualified-id before ‘>’ token
 #define  sign(s)  ((s > 0 ) ? 1 : ((s<0) ? -1 : 0))
```

이를 수정하기 위해서는 다음을 참조한다. <https://github.com/opencv/opencv_contrib/issues/618> <br/>
즉 <br/>  
```
opencv_contrib/modules/tracking/include/opencv2/tracking/onlineMIL.hpp:
#define  sign(s)  ((s > 0 ) ? 1 : ((s<0) ? -1 : 0))  ==> #define  sgn(s)  ((s > 0 ) ? 1 : ((s<0) ? -1 : 0))
```

그리고 다음을 수정한다. <br/>
```
opencv_contrib/modules/tracking/src/onlineMIL.cpp : 
310: from a sign() call to a sgn() call
339: from a sign() call to a sgn() call
```

#### if you got a error like as below during compiling caffe-ssd on intel CPU Desktop

```
/usr/include/boost/property_tree/detail/json_parser_read.hpp:257:264: error: ‘type name’ declared as function returning an array
make: *** [.build_release/cuda/src/caffe/layers/detection_output_layer.o] Error 1
```

To solve the above ,  update the gcc, g++ compiler version to above 5. refer to <https://github.com/BVLC/caffe/issues/4957>

```
$ sudo add-apt-repository ppa:ubuntu-toolchain-r/test
$ sudo apt-get update
$ sudo apt-get install gcc-5 g++-5
```

and then delete and create the gcc, g++ link 
```
$ sudo rm /usr/bin/gcc
$ sudo rm /usr/bin/g++
$ sudo cd /usr/bin
$ sudo ln -s gcc-5 gcc
$ sudo ln -s g++-5 g++
```

#### if ld can't find hdf5_serial_hl and hdf5_serial, use the old one in Makefile

```
LIBRARIES += glog gflags protobuf boost_system boost_filesystem boost_regex m hdf5_hl hdf5 boost_regex
# LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial boost_regex
```
