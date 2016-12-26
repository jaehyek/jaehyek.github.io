---
layout: post
title:  "eMMC UFS Issues 06"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- eMCP eMMC
- Controller : 
- Hy

# Failure Symptom
- no boot

# Failure procedure
- fail1 : Static Wear Leveling does not work in case that Sequential Writing continues to repeat on narrow area block
- fail2 : Static Wear Leveling does not work in case that SPO continues  to repeat after small Writing 
![001](/img/2016-12-26-eMMC-UFS-Issues-06/001.JPG)

# Cause
- fail1 
  - on clean area, not on dirty area  
  - 512KB Chunk Sequential Writing was done repeatedly on 1GB 
  - Static Wear Leveling does not work properly
![002](/img/2016-12-26-eMMC-UFS-Issues-06/002.JPG)

- fail2 
  - while valid data is full 
  - small data was written repeatedly on 1GB
  - Erase counts on Over-provision area and 1GB range was increased rapidly
  - SPO during small data writing caused the Static Wear Leveling not work properly
![003](/img/2016-12-26-eMMC-UFS-Issues-06/003.JPG)

