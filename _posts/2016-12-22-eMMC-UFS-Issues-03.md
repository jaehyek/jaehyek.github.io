---
layout: post
title:  "eMMC UFS Issues 03"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 16GB eMCP eMMC
- Controller : Venice
- SS

# Failure Symptom
- Writing via Command Queuing, and then time-out, No Reset. 

# Failure procedure
1. Writing a mass of data such Video, picture(jpeg)

# Cause
- This product use a common buffer for Meta Data and User data Garbage Collection.
- If a common buffer Meta Data  was already assigned,  additional buffer assignment caused to fail.
![001](/img/2016-12-22-eMMC-UFS-Issues-03/001.JPG)

