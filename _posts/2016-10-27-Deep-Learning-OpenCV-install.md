---
layout: post
title:  "OpenCV installation on Ubnut 14.04"
categories: Deep-Learning
comments: true
tags:  Deep-Learning OpenCV 
author: Jaehyek
---

refer to the URL <https://github.com/DrewNF/Build-Deep-Learning-Env-with-Tensorflow-Python-OpenCV>

#### Preparing Linux Machine

```
$ sudo apt-get update 
$ sudo apt-get upgrade
```

Now we need to install our developer tools:

```
$ sudo apt-get install build-essential cmake git pkg-config
```

OpenCV needs to be able to load various image file formats from disk, including JPEG, PNG, TIFF, etc. In order to load these image formats from disk, we’ll need our image I/O packages:

```
$ sudo apt-get install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev
```

how do we display the actual image to our screen? The answer is the GTK development library, which the highgui  module of OpenCV depends on to guild Graphical User Interfaces (GUIs):

```
$ sudo apt-get install libgtk2.0-dev
```

what about processing video streams and accessing individual frames? We’ve got that covered here:

```
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
```

Install libraries that are used to optimize various routines inside of OpenCV:

```
$ sudo apt-get install libatlas-base-dev gfortran
```

if a Python package manager is needed ? install pip : 

```
$ wget https://bootstrap.pypa.io/get-pip.py 
$ sudo python get-pip.py
```

#### Install a OpenCV

```
$ cd ~ $ git clone https://github.com/Itseez/opencv.git
$ cd opencv 
$ git checkout 3.0.0
```

> You can replace the 3.0.0  version with whatever the current release is. Be sure to check OpenCV.org for information on the latest release.

We also need the opencv_contrib repo as well. Without this repository, we won’t have access to standard keypoint detectors and local invariant descriptors (such as SIFT, SURF, etc.) that were available in the OpenCV 2.4.X version. We’ll also be missing out on some of the newer OpenCV 3.0 features like text detection in natural images:

```
$ cd ~ 
$ git clone https://github.com/Itseez/opencv_contrib.git 
$ cd opencv_contrib 
$ git checkout 3.0.0
```

> make sure that you checkout the same version for opencv_contrib that you did for opencv above, otherwise you could run into compilation errors

Time to setup the build:

```
$ cd ~/opencv 
$ mkdir build 
$ cd build 
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \ -D CMAKE_INSTALL_PREFIX=/usr/local \ -D INSTALL_C_EXAMPLES=ON \ -D INSTALL_PYTHON_EXAMPLES=ON \ -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \ -D BUILD_EXAMPLES=ON ..

```

Here some very important options, read carefully :

```
CMAKE_BUILD_TYPE : This option indicates that we are building a release binary of OpenCV.
CMAKE_INSTALL_PREFIX : The base directory where OpenCV will be installed.
PYTHON2_PACKAGES_PATH : The explicit path to where our site-packages  directory lives in our cv  virtual environment.
PYTHON2_LIBRARY : Path to our Hombrew installation of Python.
PYTHON2_INCLUDE_DIR : The path to our Python header files for compilation.
INSTALL_C_EXAMPLES : Indicate that we want to install the C/C++ examples after compilation.
INSTALL_PYTHON_EXAMPLES : Indicate that we want to install the Python examples after complication.
BUILD_EXAMPLES : A flag that determines whether or not the included OpenCV examples will be compiled or not.
OPENCV_EXTRA_MODULES_PATH : This option is extremely important — here we supply the path to the opencv_contrib repo 
                that we pulled down earlier, indicating that OpenCV should compile the extra modules as well.
```

> The compiling options changes depending on the version of python and most depending on how we are installing all the libraries and the dependencies.<br/>
> In order to build OpenCV 3.1.0, you need to set -D INSTALL_C_EXAMPLES=OFF (rather than ON) in the cmake command. There is a bug in the OpenCV v3.1.0 CMake build script that can cause errors if you leave this switch on. Once you set this switch to off, CMake should run without a problem.

Now we can finally compile OpenCV:

```
$ make -j4
```

Where you can replace the 4 with the number of available cores on your processor to speedup the compilation.
OpenCV Linking: If we have installed OpenCV globally on your PC and you want to link it to the virtualenv, we need to export the two following paths:

```
** export PYTHONPATH="${PYTHONPATH}:/my/other/path"** (Example of path: /opt/amd64/opencv-3.1.0/lib/python2.7/dist-packages)
** export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/my/other/path"** (Example of path: /opt/amd64/opencv-3.1.0/lib)
```

Assuming that OpenCV compiled without error, you can now install it on your Ubuntu system:

```
$ sudo make install 
$ sudo ldconfig
```

If you’ve reached this step without an error, OpenCV should now be installed in ** /usr/local/lib/python2.7/site-packages**. However, our cv virtual environment is located in our home directory — thus to use OpenCV within our cv environment, we first need to sym-link OpenCV into the site-packages directory of the cv virtual environment:

```
$ cd ~/.virtualenvs/cv/lib/python2.7/site-packages/ 
$ ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so
```

Your output should be:

```
>>> import cv2
>>> cv2.__version__ '3.0.0'
```

#### Download cuDNN 6.5

```
$ cd ~
$ wget https://s3-eu-west-1.amazonaws.com/christopherbourez/public/cudnn-6.5-linux-x64-v2.tgz
```

Add to your .bashrc

```
$ export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda-7.0/lib64:/home/users/N!OMUSUARI/cudnn-6.5-linux-x64-v2"
$ export CUDA_HOME=/usr/local/cuda-7.0
```

