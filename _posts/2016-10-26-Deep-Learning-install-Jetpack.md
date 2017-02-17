---
layout: post
title:  "install Jetpack on NVidia TX1"
categories: Deep-Learning
comments: true
tags:  Deep-Learning TX1 Jetpack 
author: Jaehyek
---


refer to the URL <https://www.youtube.com/watch?v=DyhRMjaUknQ&t=607s> <br/>
refer to the URL <https://developer.nvidia.com/embedded-computing> <br/>

#### Host PC 
- Ubuntu 14.04

####  Download the JetPack-L4T-2.3.1-linux-x64.run
- visit to https://developer.nvidia.com/embedded-computing and download 
- run it

#### Post Installation information for Jetson TX1

- Flash 64bit OS to TX1 device 
- Push and install 64bit CUDA on target
- Push and install GIE on target
- Push and install 64bit OpenCV4Tegra on target
- Push and install 64bit PerfKit on target
- Push and install 64bit cuDNN on target
- Push and install 64bit VisionWorks on target
- Push and install 64bit VisionWorks SFM on target
- Push and install 64bit VisionWorks Tracking on target
- Push and install MMAPI on target
- Cross-compile 64Bit  CUDA samples and push target

#### to enForce Recovery Mode .

> and disconnect the power adapter,  and connect USB-A to PC  <br/>
> and connect the power adapter,  <br/>
> and press the power button , after 1 second <br/>
> and press the rec button and hold it  <br/>
> and press the reset button , and release it  <br/>
> and release the rec button  <br/>

#### find the following result . 

> $ lsusb <br/>
> Bus 002 Device 002: ID 8087:8002 Intel Corp.  <br/>
> Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub <br/>
> Bus 008 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub <br/>
> Bus 007 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub <br/>
> Bus 006 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub <br/>
> Bus 005 Device 003: ID 0955:7721 NVidia Corp.  <br/>
> Bus 005 Device 002: ID 2109:3431 VIA Labs, Inc. Hub <br/>
> Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub <br/>
> Bus 001 Device 002: ID 8087:800a Intel Corp.  <br/>
> Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub <br/>
> Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub <br/>
> Bus 003 Device 003: ID 275d:0ba6   <br/>
> Bus 003 Device 002: ID 1a2c:2d23 China Resource Semico Co., Ltd  <br/>
> Bus 003 Device 004: ID 1b1c:0c04 Corsair  <br/>
> Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub <br/>


#### follow the rest instructions

