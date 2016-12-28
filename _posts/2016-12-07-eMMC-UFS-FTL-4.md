---
layout: post
title:  "eMMC & UFS FTL (4)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS FTL
author: Jaehyek
---

# MEMCON and ONFI  (Open NAND Flash Interface) <http://www.ofni.org>


### Removing the Page Register Bottleneck
- While the host is reading data from the page register, the next page could be read from the array
 - But… there is only one page register…
- The NAND vendors added a cache register to solve this issue
![001](/img/2016-12-07-eMMC-UFS-FTL-4/001.JPG)

### Multiple Plane Operations
- NAND vendors have started splitting the array into “planes” within a die
- Allows simultaneous operations of the same type to different block addresses
![002](/img/2016-12-07-eMMC-UFS-FTL-4/002.JPG)
![004](/img/2016-12-07-eMMC-UFS-FTL-4/004.JPG)
![005](/img/2016-12-07-eMMC-UFS-FTL-4/005.JPG)
![006](/img/2016-12-07-eMMC-UFS-FTL-4/006.JPG)
![007](/img/2016-12-07-eMMC-UFS-FTL-4/007.JPG)
![008](/img/2016-12-07-eMMC-UFS-FTL-4/008.JPG)
 
### Multiple Plane Read Operations
- Multiple plane read operations are when multiple reads are issued at roughly the same time
- Limitation: Page address for reads have to be the same
![003](/img/2016-12-07-eMMC-UFS-FTL-4/003.JPG)
 
 
 

