---
layout: post
title:  "eMMC UFS Issues 10"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- eMMC 
- Controller : 
- MI

# Failure Symptom
- several timeout error for mmc0 R/W operation
- Failure rate : 3/20

# Failure procedure
![001](/img/2016-12-26-eMMC-UFS-Issues-10/001.JPG)

# Root Cause
- eMMC CMD protocol analysis showed CMD 23 timeout invoke the ext4 file system error after HPI timeout by CMD13
![002](/img/2016-12-26-eMMC-UFS-Issues-10/002.JPG)
- Host MMC driver refer to out-of-interrupt busy timing value from ECSD[198]:0x0A(100ms).
After 100ms ECSD[198] value, the host MMC driver send CMD23 but timeout happens due to prg-state
- The small value of out-of-interrupt busy timing is cause of the problem 

# temporary corrective action
![003](/img/2016-12-26-eMMC-UFS-Issues-10/003.JPG)

# corrective action
- Firmware Update
