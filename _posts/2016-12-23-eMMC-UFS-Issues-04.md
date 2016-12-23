---
layout: post
title:  "eMMC UFS Issues 04"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 8GB eMCP eMMC
- Controller : 
- Hy

# Failure Symptom
- UECC
- EOL ( end of Life )
- system can not boot up 

# Failure procedure
1. Writing a fixed pattern ( all zero pattern ) Continuously
![001](/img/2016-12-22-eMMC-UFS-Issues-04/001.JPG)
2. Almost page blocks have UECC


# Cause
- The Randomize Algorithm caused to make failure 
 - Random seed of each page is assigned to each different value, but fixed
 - Writing all "O" pattern data causes writing to same page and same location. 
 - It make the cell to be faded out 
![002](/img/2016-12-22-eMMC-UFS-Issues-04/002.JPG)

