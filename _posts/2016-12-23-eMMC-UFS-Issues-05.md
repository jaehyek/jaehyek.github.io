---
layout: post
title:  "eMMC UFS Issues 05"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 8GB eMCP eMMC
- Controller : 
- Hy

# Failure Symptom
- Using Packed Command while SPO (sudden power off ) caused data disappeared 

# Failure procedure
1. Normal Case
 - At first picture, issue packed command
 - At second picture, write data seperately
![001](/img/2016-12-22-eMMC-UFS-Issues-05/001.JPG)
2. Crash Case
 - At first picture, power-off at command 7
 - At second picture, command 6 got no data 
![002](/img/2016-12-22-eMMC-UFS-Issues-05/002.JPG)

# Cause
- Normal Case 
 - First, Packed-written Data is gone to SRAM, not to NAND 
 - If same address data come in, updating will done with existing same address data
![003](/img/2016-12-22-eMMC-UFS-Issues-05/003.JPG)

![004](/img/2016-12-22-eMMC-UFS-Issues-05/004.JPG)

