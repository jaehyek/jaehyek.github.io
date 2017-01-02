---
layout: post
title:  "eMMC UFS Issues 13"
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
- Assert 시Bit Flip samples FA status

# Root Cause
- System Block Consistency FAIL
- The FTL Meta Data for Map table got a bit flip, and then FW ASSERT
- While GC for Map Block , the bit flip cause the number of vaild page mismatch not consistency
- and then produced the ASSERT 
- and then FW ASSERT while booting

![001](/img/2017-01-03-eMMC-UFS-Issues-13/001.JPG)


# Cause of bit flip
- suspection of SRAM defect
- After code review, There is no code to change the bit flip
- No defect in the Map Table Meta Data