---
layout: post
title:  "eMMC UFS Issues 11"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 16nm eMMC 4.5  4G 
- Controller : 
- Hy

# Failure Symptom
- Smart Phone hang-up, No Power-On
- Read Reclaim Fail

# Root Cause
- Read Disturbance UECC error for file "Framework.odex" , size 10.1MB
- Read count : 1.28M times 
- After E/W 0.1K, Under Read Stress Repeat Test ,  Read error over 100K times 
![001](/img/2016-12-26-eMMC-UFS-Issues-11/001.JPG)

# Mechanism of  Read Disturbance Failure
- turn on the Pass Bais to neighbor cell within same block
- turn off the Pass Bais to reading cell to read page data within same block
- can read data for the cell 
- in case that the same cell is read repeatedly, it is possible to make a read disturbance sympton 
![002](/img/2016-12-26-eMMC-UFS-Issues-11/002.JPG)

