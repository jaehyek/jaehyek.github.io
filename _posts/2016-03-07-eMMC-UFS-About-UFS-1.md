---
layout: post
title:  "eMMC & UFS About UFS (1)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS About
author: Jaehyek
---

# UFS (Universal Flash Storage)
UFS = SATA High Speed + SCSI Standardization + eMMC Low Power

JEDEC defines UFS as the next generation mobile storage spec

![001](/img/2016-12-07-eMMC-UFS-FTL-1/001.JPG)
![002](/img/2016-12-07-eMMC-UFS-FTL-1/002.JPG)
![003](/img/2016-12-07-eMMC-UFS-FTL-1/003.JPG)

#### UFS Serial Interface

- the demand for speed and cost has led to parallel communication links becoming deprecated in favor of serial links.
- Speed:
  - Clock skew reduces the speed of every link.
  - Crosstalk creates interference between the parallel lines
- Cost: The decreasing cost of integrated circuits

![004](/img/2016-12-07-eMMC-UFS-FTL-1/004.JPG)

#### UFS AsyncCommand & Command Queuing

- Set it and forget it
- Optimal for multi processing
- Support multiple CMD queuing Maximize parallel programming
- Better throughput through better NAND utilization

![005](/img/2016-12-07-eMMC-UFS-FTL-1/005.JPG)

- Re-Ordering.
  - Command queue execution sequence can be changed by considering NAND interleaving
  - Numberof active NAND chips per time is improved
  - Suitable for UFS because UFS protocol is a multi-thread, asynchronous protocol
  
#### UFS has bette features than eMMC

Items | eMMC | UFS
----|-----|----
Transfer scheme | Sync | Async
Command Queue | No(Yes for eMMC5.1) Packed Commands | Yes 32-Queue Depths
State | State Transition | Stateless
Interface | Parallel/Half-Duplex | Serial / Full-Duplex 
Priority | No | SCSI Command Priority Higher-Priority LU
Abort Scheme | HPI | Task Management Scheme
Features | Legacy eMMCFunctions | Same with eMMC
Command Set | Legacy eMMCCommands | SCSI Commands
Partitions | Boot/RPMB/User Area | 8-LU(including Boot)/ RPMB

