---
layout: post
title:  "eMMC & UFS FTL (2)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS FTL
author: Jaehyek
---

# GC & Write Amplification

### Garbage collection
- FTL fills incoming data into the erased nand-block
 - Overwriting the same logical block goes to new erase nand block ( copy on write)
![001](/img/2016-12-07-eMMC-UFS-FTL-2/001.JPG)

- No free space => Do GC
 - Copy valid pages
![002](/img/2016-12-07-eMMC-UFS-FTL-2/002.JPG)

- Copy done !!
![003](/img/2016-12-07-eMMC-UFS-FTL-2/003.JPG)

- Erase 5 blocks, GC done
![004](/img/2016-12-07-eMMC-UFS-FTL-2/004.JPG)

- Performance degradation by GC
![005](/img/2016-12-07-eMMC-UFS-FTL-2/005.JPG)

### Write amplification
- Write amplification = ( Data written to the flash memory) / ( Data written by host )
- WA KEY = Garbage collection Map(FTL-meta) update Wear-leveling

