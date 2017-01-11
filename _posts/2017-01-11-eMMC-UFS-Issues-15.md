---
layout: post
title:  "eMMC UFS Issues 15"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 
- Controller : 
- Hy

# Failure Symptom
- Encryption Screen pop-up when power on.

# Root Cause
- read time out(10ms) at RPMB ( Replay Protect Memory Block )

# Cause procedure
1. encryption key is saved in RPMB for FDE(Full-disk Encryption)
2. When mount the user data region , it time-over to read-out the RPMB encryption key

* At Android M-OS, the timeout max value  was set to 150mS.
* At Android N-OS, it was failed.

* FDE(Full-disk Encryption) : The User data partition was encripted with Encryption key for the protection of Hacking,
   and the Encryption key was saved to eMMC RPMB block. when mount the partition it was descripted with Encryption key.
