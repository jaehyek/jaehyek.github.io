---
layout: post
title:  "Install Tensorflow on Windows"
categories: Deep-Learning
comments: true
tags:  Deep-Learning Tensorflow Windows
author: Jaehyek
---

다음의 내용은 [여기](http://tmmse.xyz/2017/03/01/tensorflow-keras-installation-windows-linux-macos/)을 참조하자.

1. Anaconda 설치
2. CUDA설치 ( https://developer.nvidia.com/cuda-downloads )
3. cuDNN 설치 ver 8.0
 경로 추가 : c:\Program Files\NVIDiA GPU Computing Toolkit\CUDA\v8.0
4. 관리자 권한에서 다음 실행.
  conda create -n tensorflow_in_cpu python=3.5
 혹은
  conda create -n tensorflow_in_gpu python=3.5
5. conda 환경 만든 곳에 tensorflow 설치하기
  activate tensorflow_in_cpu
  pip install tensorflow  ( 오류시 pip install tensorflow=0.12.1)
  혹은 
  activate tensorflow_in_gpu
  pip install tensorflow-gpu 
  ** pip3으로도 설치가능.
# 여기서부터 (tensorflow_in_cpu) 환경. 설치 순서 중요
6. Pycharm에서 tensorflow project만들기
  c:\Anaconda3\envs\tensorflow(_in_cpu)\python.exe을 선택
7. tensorflow 버전을 업데이트 시키고 싶다면
  - activate로 conda환경 들어 가신 후
  - pip install --upgrade tensorflow 혹은 
    pip install --upgrade tensorflow-gpu

conda install pandas matplotlib scikit-learn  
pip install keras  
conda install jupyter notebook