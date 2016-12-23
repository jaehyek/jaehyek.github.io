---
layout: post
title:  "eMMC UFS Issues 02"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 32GB UFS
- Controller : Siena
- SS

# Failure Symptom
- Sudden-Power-Off Test
- Booting fail

# Failure procedure
1. Check the Boot LU Size ( BOOT1:32MB, BOOT2:8MB )
2. Meta Open if the Boot LU Size is over 8MB
3. While Meta Open, read the boot data for Read-Reclaim processing for Garbage Collection 

# Cause
- Before fDeviceInit, 
- Race-condition occurs for Buffer allocation between Garbage Collection and Boot Data Read 
![001](/img/2016-12-22-eMMC-UFS-Issues-02/001.JPG)

