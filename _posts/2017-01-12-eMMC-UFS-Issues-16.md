---
layout: post
title:  "eMMC UFS Issues 16"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 
- Controller : 
- Mi

# Failure Symptom
- After 2529 cycles of overall 5000 cycles, this bit crash happened at 1 sample among total 10 samples

# Test Scenario
- Write a promised data pattern with cache/packed feature disabled
- Perform a sudden power loss at random timing
- Check a the written data after power on. If the data is different from promised pattern, the test fails

# Data Corruption after Suddern Power Off
![001](/img/2017-01-12-eMMC-UFS-Issues-16/001.JPG)

The Picture shows the data of last 3 write command was mismatched 

# Root Cause
![002](/img/2017-01-12-eMMC-UFS-Issues-16/002.JPG)

- A sudden Power Loss hits the page line programming including block 67/page 512/CE3 and block 68/page 1/CE0&CE1&CE2
- The only data in block 67/page 512/CE3 becomes uncorrectable after booting up 
- When scanning MLC Block 68, FW lack of vision on MLC block 67, which was hit by power loss. So FW would not discard the data in block 68 to avoid response host data pattern as new+old+new