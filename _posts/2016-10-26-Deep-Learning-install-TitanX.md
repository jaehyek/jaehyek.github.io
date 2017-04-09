---
layout: post
title:  "install Titan X on Ubuntu 14.04"
categories: Deep-Learning
comments: true
tags:  Deep-Learning summary hunkim github
author: Jaehyek
---


refer to the URL <http://www.nvidia.com/object/gpu-accelerated-applications-tensorflow-installation.html>

만일 위의 URL이 잘 되지 않는다면 다음 URL을 활용한다. <https://github.com/uher/InstallGpuEnableTensorflow>

#### Step 1. Install NVIDIA CUDA
> - download cuda_8.0.44_linux.run from <https://developer.nvidia.com/cuda-downloads>
> - download NVIDIA-Linux-x86_64-375.39.run from <http://www.nvidia.com/download/driverResults.aspx/114708/en-us>
> - run the following instructions. refer to <http://askubuntu.com/questions/848221/installing-cuda-8-0-on-ubuntu-16-04-with-nvidia-geforce-845m>
> 
> 1. sudo apt-get purge  nvidia-*
> 2. sudo service lightdm stop
> 3. sudo ./NVIDIA-Linux-x86_64-367.57.run \--no-opengl-files <br/>
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

Additionally 

> $ sudo apt-get install git <br/>
> $ sudo apt-get install vim <br/>

 
#### Step 3. Install and upgrade PIP
> $ sudo apt-get install python-pip python-dev <br/>
> $ pip install --upgrade pip <br/>
> $ sudo pip install numpy <br/>

#### Step 4. Install Bazel
To build TensorFlow from source, the Bazel build system must first be installed as follows  <br/>

> $ sudo apt-get install software-properties-common swig  <br/>
> $ sudo add-apt-repository ppa:webupd8team/java  <br/>
> $ sudo apt-get update  <br/>
> $ sudo apt-get install oracle-java8-installer  <br/>
> $ echo "deb http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list  <br/>
> $ curl https://storage.googleapis.com/bazel-apt/doc/apt-key.pub.gpg | sudo apt-key add -  <br/>
> $ sudo apt-get update  <br/>

이후 다음을 하는 것 보다 <br/>
> $ sudo apt-get install bazel <br/>

아래를 하는 것이 더 최신의 것 임.

> $ wget https://github.com/bazelbuild/bazel/archive/0.3.2.tar.gz <br/>
> $ tar -xvzf 0.3.2.tar.gz <br/>
> $ cd bazel-0.3.2/ <br/>
> $ sudo ./compile.sh <br/>
> $ sudo cp output/bazel /usr/local/bin <br/>
> $ cd .. <br/>

#### Step 5. Install TensorFlow
To obtain the best performance with TensorFlow we recommend building it from source. <br/>
First, clone the TensorFlow source code repository:  <br/>


> $ git clone https://github.com/tensorflow/tensorflow <br/>
> $ cd tensorflow  <br/>

다음을 하는 것 보다  <br/>
> $ git reset --hard 70de76e  <br/>

아래를 하는 것이 더 안정적인 것 임.

> $ git reset --hard 287db3a  <br/> 

그리고 configure을 하기 전에 다음을 실행한다.  <br/>
1.computecpp을 설치한다. 다음을 참조하고 <https://www.codeplay.com/products/computesuite/computecpp> <br/>
tar을 풀어서  /usr/local 밑에 둔다. <br/>

2.zlib_archive의 new version을 설치한다. 다음과 같이 수정한다. <https://github.com/tensorflow/tensorflow/issues/6594>

>    edit tensorflow/workspace.bzl <br/>
>    replace zlib-1.2.8 with zlib-1.2.11 <br/>
>    remove the sha256 line <br/>

혹은 

>  diff --git a/tensorflow/workspace.bzl b/tensorflow/workspace.bzl <br/>
>  index 06e16cd..7c7b44c 100644 <br/>
>  --- a/tensorflow/workspace.bzl <br/>
>  +++ b/tensorflow/workspace.bzl <br/>
>  @@ -228,9 +228,8 @@ def tf_workspace(path_prefix = "", tf_repo_name = ""): <br/>
>    <br/>
>     native.new_http_archive( <br/>
>       name = "zlib_archive", <br/>
>  -    url = "http://zlib.net/zlib-1.2.8.tar.gz", <br/>
>  -    sha256 = "36658cb768a54c1d4dec43c3116c27ed893e88b02ecfcb44f2166f9c0b7f2a0d", <br/>
>  -    strip_prefix = "zlib-1.2.8", <br/>
>  +    url = "http://zlib.net/zlib-1.2.11.tar.gz", <br/>
>  +    strip_prefix = "zlib-1.2.11", <br/>
>       build_file = str(Label("//:zlib.BUILD")), <br/>
>     ) <br/>

configure script 실행에서  "Do you wish to build TensorFlow with GPU support?" 을 질문하지 않을 수 있으므로  <br/>
export TF_NEED_CUDA = 1  하고  ( .bashrc 에 반영할 것. )  <br/>

Then run the configure script as follows:

> $ cd tensorflow <br/>
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

Then call bazel to build the TensorFlow pip package: <br/>
만일 아래의 command가  안될 때는  <br/>
bazel clean  <br/>
을 실행하고 다시 실행할 것. <br/>
 
> bazel build -c opt --config=cuda //tensorflow/tools/pip_package:build_pip_package  <br/>
> bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg <br/>

And finally install the TensorFlow pip package

> sudo pip install --upgrade /tmp/tensorflow_pkg/tensorflow-0.12* <br/>

#### Step 6. UPGRADE PROTOBUF

> 텐서플로우 pip 패키지는 protobuf pip 패키지 버전 3.0.0b2를 필요로 합니다. PyPI에서 다운받을 수 있는(pip install protobuf를 사용해서) Protobuf의 pip 패키지는 파이썬 만으로 개발된 라이브러리로 C++ 구현보다 직렬화/역직렬화시 10~50배 느립니다. Protobuf는 빠른 프로토콜 파싱을 위한 C++ 바이너리 확장을 지원합니다. 이 확장은 표준 파이썬 PIP 패키지에는 포함되어 있지 않습니다. 우리는 이 바이너리 확장을 포함한 protobuf pip 패키지를 자체적으로 만들었습니다. 다음 명령을 사용해 자체적으로 만든 protobuf pip 패키지를 설치할 수 있습니다:


Upgrade to the latest version of the protobuf package:

Python 2.7: 

> $ sudo pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.0.0b2.post2-cp27-none-linux_x86_64.whl 

Python 3.4: <br/>

> $ sudo pip3 install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.0.0b2.post2-cp34-none-linux_x86_64.whl

> cd ..

> pip install tensorflow 명령은 파이썬으로된 기본 pip 패키지를 설치하므로 위 패키지를 설치하려면 반드시 텐서플로우를 설치하고 난 후에 합니다. 위 pip 패키지는 이미 설치된 protobuf 패키지를 덮어 씁니다. 바이너리 pip 패키지는 64M 넘는 메세지에 대한 지원을 이미 하고 있어 아래와 같은 에러가 이미 해결 되었습니다:

```
[libprotobuf ERROR google/protobuf/src/google/protobuf/io/coded_stream.cc:207] A
protocol message was rejected because it was too big (more than 67108864 bytes).
To increase the limit (or to disable these warnings), see
CodedInputStream::SetTotalBytesLimit() in google/protobuf/io/coded_stream.h.
```

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
 
TensorFlow의 구현 코드(TensorFlow implementation)를 통해 graph에 정의된 내용이 실행가능한 작업들(operation)로 변환되고 CPU나 GPU같이 이용가능한 연산 자원들에 뿌려집니다. 코드로 어느 CPU 혹은 GPU를 사용할 지 명시적으로 지정할 필요는 없습니다. 작업을 가능한 한 많이 처리하기 위해 TensorFlow는 (컴퓨터가 GPU를 가지고 있다면) 첫 번째 GPU를 이용하니까요.

만약 컴퓨터에 복수의 GPU가 있어서 이를 사용하려면, op을 어느 하드웨어에 할당할 지 명시적으로 밝혀야 합니다. 작업에 사용할 CPU 혹은 GPU를 지정하려면 with...Device 구문을 사용하면 됩니다.

```
with tf.Session() as sess:
  with tf.device("/gpu:1"):
    matrix1 = tf.constant([[3., 3.]])
    matrix2 = tf.constant([[2.],[2.]])
    product = tf.matmul(matrix1, matrix2)
    ...
```

이용할 CPU 혹은 GPU는 문자열로 지정할 수 있습니다. 현재 지원되는 것은 아래와 같습니다.

```
- "/cpu:0": 컴퓨터의 CPU.
- "/gpu:0": 컴퓨터의 1번째 GPU.
- "/gpu:1": 컴퓨터의 2번쨰 GPU.
```

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

