---
layout: post
title:  "Titan X install on Ubuntu 16.04"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---

## Titan X install on Ubuntu 16.04
refer to the URL <http://www.nvidia.com/object/gpu-accelerated-applications-tensorflow-installation.html>

#### Step 1. Install NVIDIA CUDA
- download cuda_8.0.44_linux.run from <https://developer.nvidia.com/cuda-downloads>
- download NVIDIA-Linux-x86_64-367.57.run from <http://www.nvidia.com/Download/driverResults.aspx/108586/en-us>
- run the following instructions. refer to <http://askubuntu.com/questions/848221/installing-cuda-8-0-on-ubuntu-16-04-with-nvidia-geforce-845m>

1. sudo apt-get --purge remove nvidia-*
2. sudo service lightdm stop
3. sudo ./NVIDIA-Linux-x86_64-367.57.run --no-opengl-files
4. sudo ./cuda_8.0.44_linux.run **(you should not install its own nvidia-driver 367.48, as you have 367.57 already installed)**
5. in /usr/local/cuda-8.0/include/host_config.h, comment this line out: #error -- unsupported GNU version! gcc versions later than 5 are not supported!
6. insert the following in .bashrc 
export PATH=/usr/local/cuda-8.0/bin:.:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH
export GLPATH=/usr/lib   
7. reboot

#### Step 2. Install NVIDIA cuDNN
- download cudnn-8.0-linux-x64-v5.1.tgz from <https://developer.nvidia.com/rdp/cudnn-download>
- sudo tar -xvf cudnn-8.0-linux-x64-v5.1.tgz -C /usr/local
 
#### Step 3. Install and upgrade PIP
- sudo apt-get install python-pip python-dev
- pip install --upgrade pip

#### TensorFlow 1.0.0-RC0 Release

'''
@@@@@ 파이썬 2.7
@ Ubuntu/Linux 64-bit, CPU only, Python 2.7
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp27-none-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, GPU enabled, Python 2.7
@ Requires CUDA toolkit 8.0 and CuDNN v5.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp27-none-linux_x86_64.whl

@ Mac OS X, CPU only, Python 2.7:
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0rc0-py2-none-any.whl

@ Mac OS X, GPU enabled, Python 2.7:
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0rc0-py2-none-any.whl

@@@@@ 파이썬 3.x 
@ Ubuntu/Linux 64-bit, CPU only, Python 3.3
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp33-cp33m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, GPU enabled, Python 3.3
@ Requires CUDA toolkit 8.0 and CuDNN v5.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp33-cp33m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, CPU only, Python 3.4
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp34-cp34m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, GPU enabled, Python 3.4
@ Requires CUDA toolkit 8.0 and CuDNN v5.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp34-cp34m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, CPU only, Python 3.5
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp35-cp35m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, GPU enabled, Python 3.5
@ Requires CUDA toolkit 8.0 and CuDNN v5.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp35-cp35m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, CPU only, Python 3.6
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0rc0-cp36-cp36m-linux_x86_64.whl

@ Ubuntu/Linux 64-bit, GPU enabled, Python 3.6
@ Requires CUDA toolkit 8.0 and CuDNN v5.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0rc0-cp36-cp36m-linux_x86_64.whl

@ Mac OS X, CPU only, Python 3.4 or 3.5:
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0rc0-py3-none-any.whl

@ Mac OS X, GPU enabled, Python 3.4 or 3.5:
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0rc0-py3-none-any.whl

@@@@ 설치
$ sudo pip install --upgrade $TF_BINARY_URL
'''

- 윈도우즈 CPU:
'''
C:\> pip install --upgrade https://storage.googleapis.com/tensorflow/windows/cpu/tensorflow-1.0.0rc0-cp35-cp35m-win_amd64.whl
'''

- 윈도우즈 GPU:
'''
C:\> pip install --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.0.0rc0-cp35-cp35m-win_amd64.whl
'''
