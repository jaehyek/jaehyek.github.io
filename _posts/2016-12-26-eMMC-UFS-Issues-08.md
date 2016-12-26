---
layout: post
title:  "eMMC UFS Issues 08"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 64GB UFS 2.1  3D 
- Controller : 
- Hy

# Failure Symptom
- Under lower temperature ( -30 degree )
- Enter the Sleep Mode 
- Enter/Exit  Fail

# Failure procedure
- The NMOS TR Vt increment of  PLL (Phase Locked Loop) circuit  within  UFS controller does not work properly
- Inspecting Device Tx data line Eye diagram, the lower temperature jitter value was not work properly
![001](/img/2016-12-26-eMMC-UFS-Issues-08/001.JPG)
![004](/img/2016-12-26-eMMC-UFS-Issues-08/004.JPG)

# Cause
- caused by the thickness increment of TR gate oxide during foundry Fab.(TSMC, 28nm) 
![002](/img/2016-12-26-eMMC-UFS-Issues-08/002.JPG)
![003](/img/2016-12-26-eMMC-UFS-Issues-08/003.JPG)


