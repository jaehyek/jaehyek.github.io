---
layout: post
title:  "Titan X install on Ubuntu 14.04"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---


refer to the URL <http://www.nvidia.com/object/gpu-accelerated-applications-tensorflow-installation.html>

#### Step 1. Install NVIDIA CUDA
> - download cuda_8.0.44_linux.run from <https://developer.nvidia.com/cuda-downloads>
> - download NVIDIA-Linux-x86_64-367.57.run from <http://www.nvidia.com/Download/driverResults.aspx/108586/en-us>
> - run the following instructions. refer to <http://askubuntu.com/questions/848221/installing-cuda-8-0-on-ubuntu-16-04-with-nvidia-geforce-845m>
> 
> 1. sudo apt-get purge  nvidia-*
> 2. sudo service lightdm stop
> 3. sudo ./NVIDIA-Linux-x86_64-367.57.run --no-opengl-files <br/>
>    다음 step 4에서 설치할 driver을 미리 설치한다. 즉 다음 step에서는 driver을 설치하지 않아야 한다.
> 4. sudo ./cuda_8.0.44_linux.run **(you should not install its own nvidia-driver 367.48, as you have 367.57 already installed)**
> 5. in /usr/local/cuda-8.0/include/host_config.h, comment this line out: <br/>
>    #error -- unsupported GNU version! gcc versions later than 5 are not supported! <br/>
> 6. insert the following in .bashrc  <br/>
> export PATH=/usr/local/cuda-8.0/bin:.:$PATH <br/>
> export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH <br/>
> export GLPATH=/usr/lib    <br/>
> 7. reboot

#### Step 2. Install NVIDIA cuDNN
> - download cudnn-8.0-linux-x64-v5.1.tgz from <https://developer.nvidia.com/rdp/cudnn-download> <br/>
> $ sudo tar -xvf cudnn-8.0-linux-x64-v5.1.tgz -C /usr/local <br/>
 
#### Step 3. Install and upgrade PIP
> $ sudo apt-get install python-pip python-dev <br/>
> $ sudo pip install --upgrade pip <br/>

#### Step 4. Install Bazel
To build TensorFlow from source, the Bazel build system must first be installed as follows  <br/>

> $ sudo apt-get install software-properties-common swig  <br/>
> $ sudo add-apt-repository ppa:webupd8team/java  <br/>
> $ sudo apt-get update  <br/>
> $ sudo apt-get install oracle-java8-installer  <br/>
> $ echo "deb http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list  <br/>
> $ curl https://storage.googleapis.com/bazel-apt/doc/apt-key.pub.gpg | sudo apt-key add -  <br/>
> $ sudo apt-get update  <br/>
> $ sudo apt-get install bazel <br/>

#### Step 5. Install TensorFlow
To obtain the best performance with TensorFlow we recommend building it from source. <br/>
First, clone the TensorFlow source code repository:  <br/>

> $ git clone https://github.com/tensorflow/tensorflow <br/>
> $ cd tensorflow  <br/>
> $ git reset --hard 70de76e  <br/>

Then run the configure script as follows:

> $ ./configure  <br/>
> Please specify the location of python. [Default is /usr/bin/python]: [enter] <br/>
> Do you wish to build TensorFlow with Google Cloud Platform support? [y/N] n  <br/>
> No Google Cloud Platform support will be enabled for TensorFlow  <br/>
> Do you wish to build TensorFlow with GPU support? [y/N] y  <br/>
> GPU support will be enabled for TensorFlow  <br/>
> Please specify which gcc nvcc should use as the host compiler. [Default is /usr/bin/gcc]: [enter]  <br/>
> Please specify the Cuda SDK version you want to use, e.g. 7.0. [Leave empty to use system default]: 8.0  <br/>
> Please specify the location where CUDA 8.0 toolkit is installed. Refer to README.md for more details. [Default is /usr/local/cuda]: [enter]  <br/>
> Please specify the Cudnn version you want to use. [Leave empty to use system default]: 5  <br/>
> Please specify the location where cuDNN 5 library is installed. Refer to README.md for more details. [Default is /usr/local/cuda]: [enter]  <br/>
> Please specify a list of comma-separated Cuda compute capabilities you want to build with.  <br/>
> You can find the compute capability of your device at: https://developer.nvidia.com/cuda-gpus.  <br/>
> Please note that each additional compute capability significantly increases your build time and binary size.  <br/>
> [Default is: "3.5,5.2"]: 5.2,6.1 [see https://developer.nvidia.com/cuda-gpus]  <br/>
> Setting up Cuda include  <br/>
> Setting up Cuda lib64  <br/>
> Setting up Cuda bin  <br/>
> Setting up Cuda nvvm  <br/>
> Setting up CUPTI include  <br/>
> Setting up CUPTI lib64  <br/>
> Configuration finished <br/>

Then call bazel to build the TensorFlow pip package:
 
> bazel build -c opt --config=cuda //tensorflow/tools/pip_package:build_pip_package  <br/>
> bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg <br/>

And finally install the TensorFlow pip package

Python 2.7: <br/>

> $ sudo pip install --upgrade /tmp/tensorflow_pkg/tensorflow-0.9.0-*.whl 


Python 3.4: <br/>

> $ sudo pip install --upgrade /tmp/tensorflow_pkg/tensorflow-0.9.0-*.whl

#### Step 6. UPGRADE PROTOBUF
Upgrade to the latest version of the protobuf package:

Python 2.7: <br/>

> $ sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.0.0b2.post2-cp27-none-linux_x86_64.whl 

Python 3.4: <br/>

> $ sudo pip3 install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.0.0b2.post2-cp34-none-linux_x86_64.whl

#### Step 7. TEST YOUR INSTALLATION
To test the installation, open an interactive Python shell and import the TensorFlow module:

> $ cd  <br/>
> $ python  <br/>
> …  <br/>
> import tensorflow as tf  <br/>
> I tensorflow/stream_executor/dso_loader.cc:105] successfully opened CUDA library libcublas.so locally  <br/>
> I tensorflow/stream_executor/dso_loader.cc:105] successfully opened CUDA library libcudnn.so locally  <br/>
> I tensorflow/stream_executor/dso_loader.cc:105] successfully opened CUDA library libcufft.so locally  <br/>
> I tensorflow/stream_executor/dso_loader.cc:105] successfully opened CUDA library libcuda.so.1 locally  <br/>
> I tensorflow/stream_executor/dso_loader.cc:105] successfully opened CUDA library libcurand.so locally <br/>

With the TensorFlow module imported, the next step to test the installation is to create a TensorFlow Session, which will initialize the available computing devices and provide a means of executing computation graphs:

> sess = tf.Session()

This command will print out some information on the detected hardware configuration. For example, the output on a system containing a Tesla M40 GPU is:

>  sess = tf.Session()  <br/>
> I tensorflow/core/common_runtime/gpu/gpu_init.cc:102] Found device 0 with properties:  <br/>
> name: Tesla M40  <br/>
> major: 5 minor: 2 memoryClockRate (GHz) 1.112  <br/>
> pciBusID 0000:04:00.0  <br/>
> Total memory: 11.25GiB  <br/>
> Free memory: 11.09GiB  <br/>
> …

To manually control which devices are visible to TensorFlow, set the CUDA_VISIBLE_DEVICES environment variable when launching Python. For example, to force the use of only GPU 0:

> $ CUDA_VISIBLE_DEVICES=0 python

You should now be able to run a Hello World application:

> hello_world = tf.constant("Hello, TensorFlow!")  <br/>
> print sess.run(hello_world)  <br/>
> Hello, TensorFlow!  <br/>
> print sess.run(tf.constant(123)*tf.constant(456))  <br/>
> 56088 <br/>
 

#### TensorFlow 1.0.0-RC0 Release
아래의 글은 <https://tensorflow.blog/2017/01/27/tensorflow-1-0-0-rc0-release/>에서 퍼 온 글이다.

> ## 파이썬 2.7
> # Ubuntu/Linux 64-bit, CPU only, Python 2.7 <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp27-none-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, GPU enabled, Python 2.7 <br/>
> # Requires CUDA toolkit 8.0 and CuDNN v5. <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp27-none-linux_x86_64.whl

> ##### # Mac OS X, CPU only, Python 2.7: <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0rc0-py2-none-any.whl

> ##### # Mac OS X, GPU enabled, Python 2.7: <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0rc0-py2-none-any.whl

> ## 파이썬 3.x 
> # Ubuntu/Linux 64-bit, CPU only, Python 3.3 <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp33-cp33m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, GPU enabled, Python 3.3 <br/>
> # Requires CUDA toolkit 8.0 and CuDNN v5. <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp33-cp33m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, CPU only, Python 3.4 <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp34-cp34m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, GPU enabled, Python 3.4 <br/>
> # Requires CUDA toolkit 8.0 and CuDNN v5. <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp34-cp34m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, CPU only, Python 3.5 <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp35-cp35m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, GPU enabled, Python 3.5 <br/>
> # Requires CUDA toolkit 8.0 and CuDNN v5. <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp35-cp35m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, CPU only, Python 3.6 <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp36-cp36m-linux_x86_64.whl

> ##### # Ubuntu/Linux 64-bit, GPU enabled, Python 3.6 <br/>
> # Requires CUDA toolkit 8.0 and CuDNN v5. <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp36-cp36m-linux_x86_64.whl

> ##### # Mac OS X, CPU only, Python 3.4 or 3.5: <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0rc0-py3-none-any.whl

> ##### # Mac OS X, GPU enabled, Python 3.4 or 3.5: <br/>
> $ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0rc0-py3-none-any.whl

> ## 설치 <br/>
> $ sudo pip install --upgrade $TF_BINARY_URL


- 윈도우즈 CPU:

> C:\> pip install --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.0.0rc0-cp35-cp35m-win_amd64.whl


- 윈도우즈 GPU:

> C:\> pip install --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.0.0rc0-cp35-cp35m-win_amd64.whl

