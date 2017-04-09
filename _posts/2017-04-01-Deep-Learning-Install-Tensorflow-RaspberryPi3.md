---
layout: post
title:  "Install Tensorflow on Raspberry PI 3"
categories: Deep-Learning
comments: true
tags:  Deep-Learning Tensorflow Raspberry
author: Jaehyek
---

다음의 내용은 Raspberry PI 3 에 Tensorflow을 설치하는 순서를 알려준다. 

1. <https://ubuntu-mate.org/raspberry-pi/> 에서  Ubuntu Mate을 설치한다.
    기본적으로 Python 2.7, 3.5 가 설치되어 있다.
    arm7l 용으로 build 되어 있는 tensorflow는 <https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/>
    에서 구할 수 있는 데 Python 3.4이다. 
    ( Python 3.5용은 별도로 compile해야 하므로 시간이 많이 걸린다. 거의 할 수 없다. )
    해서 miniconda을 설치하면서 Python 3.4을 설치하고 tensorflow for Python 3.4을 설치한다.
    
2. miniconda을 설치한다. 
    <https://repo.continuum.io/miniconda/> 에서 Miniconda3-3.16.0-Linux-armv7l.sh 을 다운 받는다.
    <https://www.continuum.io/blog/developer/anaconda-raspberry-pi> 을 참조하면, 
    $ wget http://repo.continuum.io/miniconda/Miniconda3-3.16.0-Linux-armv7l.sh
    $ md5sum Miniconda3-3.16.0-Linux-armv7l.sh
    $ /bin/bash Miniconda3-3.16.0-Linux-armv7l.sh
    
3. path에 conda/bin을 추가한다. 

> export PATH="/home/jaehyek/miniconda3/bin:$PATH"
   
4. Tensorflow 을 설치한다.
    <https://github.com/samjabrahams/tensorflow-on-raspberry-pi>을 참조하여 설치한다. 
    
> $ sudo apt-get update
> 
> # For Python 3.4
> $ sudo apt-get install python3-pip python3-dev
> 
> $ wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.0.1/tensorflow-1.0.1-cp34-cp34m-linux_armv7l.whl
> $ pip3 install --user tensorflow-1.0.1-cp34-cp34m-linux_armv7l.whl