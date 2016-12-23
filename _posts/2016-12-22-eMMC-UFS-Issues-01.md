---
layout: post
title:  "eMMC UFS Issues 01"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 8GB eMCP, TLC
- Controller : VPX
- SS

# Failure Symptom
- Can not perform the emmc command "CMD23"

# Failure procedure
1. Known data write
2. ( random write 4K x 3500 times  Sleep  Resume) x 50K times
3. UECC check
4. Sequential write


# Cause
- was caused by EOL ( End of Life)
![001](/img/2016-12-22-eMMC-UFS-Issues-01/001.JPG)
- was caused by frequently Random Write
- was caused by frequently MetaData Update
![002](/img/2016-12-22-eMMC-UFS-Issues-01/002.JPG)
![003](/img/2016-12-22-eMMC-UFS-Issues-01/003.JPG)

# SS Quality Criteria

### Test Pattern of DWL @ Samsung(Write Amount Ratio)

Classification | Chunk Size | Write Amount Ratio
-----|----|----
Random Write | 4K/8K | 5%
Seq Write | 16K/32K~4M | 35%
Download | 4M | 60%

### WAI(Wear Acceleration Index) – Index which indicate Meta lifespan by host write amount

item | WAI with Samsung TBW Pattern | WAI with 4K Random Write Pattern
-----|----|----
SLC WAI | 0.28 | 22.96


