---
layout: post
title:  "Install Tensorflow and Opencv on Raspberry PI 3"
categories: Deep-Learning
comments: true
tags:  Deep-Learning Tensorflow Raspberry
author: Jaehyek
---

다음의 내용은 Raspberry PI 3 에 Tensorflow을 설치하는 순서를 알려준다. 

1. <https://ubuntu-mate.org/raspberry-pi/> 에서  Ubuntu Mate을 설치한다. <br/>
    기본적으로 Python 2.7, 3.5 가 설치되어 있다. <br/>
    arm7l 용으로 build 되어 있는 tensorflow는 <https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/> <br/>
    에서 구할 수 있는 데 Python 3.4이다.  <br/>
    ( Python 3.5용은 별도로 compile해야 하므로 시간이 많이 걸린다. 거의 할 수 없다. ) <br/>
    해서 miniconda을 설치하면서 Python 3.4을 설치하고 tensorflow for Python 3.4을 설치한다. <br/>
    
2. miniconda을 설치한다.  <br/>
    <https://repo.continuum.io/miniconda/> 에서 Miniconda3-3.16.0-Linux-armv7l.sh 을 다운 받는다. <br/>
    <https://www.continuum.io/blog/developer/anaconda-raspberry-pi> 을 참조하면,  <br/>
    
> $ wget http://repo.continuum.io/miniconda/Miniconda3-3.16.0-Linux-armv7l.sh <br/>
> $ md5sum Miniconda3-3.16.0-Linux-armv7l.sh <br/>
> $ /bin/bash Miniconda3-3.16.0-Linux-armv7l.sh
    
3. path에 conda/bin을 추가한다. 

> export PATH="/home/jaehyek/miniconda3/bin:$PATH"
   
4. Tensorflow 을 설치한다. <br/>
    <https://github.com/samjabrahams/tensorflow-on-raspberry-pi>을 참조하여 설치한다. 
    
> $ sudo apt-get update
> 
> ***For Python 3.4***
> $ sudo apt-get install python3-pip python3-dev
> 
> $ wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.0.1/tensorflow-1.0.1-cp34-cp34m-linux_armv7l.whl <br/>
> $ pip3 install --user tensorflow-1.0.1-cp34-cp34m-linux_armv7l.whl <br/>

5. OpenCV을 설치한다.  <br/>
   <http://www.emindlab.com/raspberry-pi/opencv-3-1-0-raspberry-pi.html> 여기를 참조한다.
   
```
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install guvcview synaptic python-dev python-numpy python-scipy python-matplotlib 
sudo apt-get install python-pandas python-nose build-essential cmake pkg-config
sudo apt-get install default-jdk ant libgtkglext1-dev bison libqt4-dev-tools libqt4-dev libqt4-core libqt4-gui v4l-utils
sudo apt-get install qtcreator

sudo wget http://liquidtelecom.dl.sourceforge.net/project/opencvlibrary/opencv-unix/3.1.0/opencv-3.1.0.zip
sudo unzip opencv-3.1.0.zip
cd opencv-3.1.0
sudo mkdir build
cd build

sudo cmake -D CMAKE_BUILD_TYPE=RELEASE -D INSTALL_C_EXAMPLES=ON –D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON 
 -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_OPENGL=ON -D WITH_V4L=ON –D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_TBB=ON ..
sudo make
sudo make install
sudo nano /etc/ld.so.conf.d/opencv.conf
/usr/local/lib

Press Control + X to save

sudo ldconfig

sudo nano /etc/bash.bashrc

export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig


cd opencv-3.1.0/samples/cpp

g++ -o facedetect facedetect.cpp `pkg-config opencv --cflags --libs`

./facedetect

https://docs.google.com/document/d/1OcVoQi8UJ2bCtJ2nFPkI-eZi9kuQoqthpOwpCpLGwJE/edit?usp=sharing

```