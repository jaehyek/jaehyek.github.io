---
layout: post
title:  "eMMC & UFS About UFS (1)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS About
author: Jaehyek
---
The following information was astracted from 

[UFS_Overview_20150821_r0.pdf](/attach/ppt/2016-03-07-eMMC-UFS-About-UFS-1/UFS_Overview_20150821_r0.pdf)

[M1CCL02-082_Toshiba_UFS_Memory_Overview_for_LGMC_20151022m(S).pdf](/attach/ppt/2016-03-07-eMMC-UFS-About-UFS-1/M1CCL02-082_Toshiba_UFS_Memory_Overview_for_LGMC_20151022m(S).pdf)

[M1PCA00-010_TOSHIBA_UFS_Ver2.0_Application_Note_Rev0.1.pdf](/attach/ppt/2016-03-07-eMMC-UFS-About-UFS-1/M1PCA00-010_TOSHIBA_UFS_Ver2.0_Application_Note_Rev0.1.pdf)

[151024_Samsung_Flash_Memory.pdf](/attach/ppt/2016-03-07-eMMC-UFS-About-UFS-1/151024_Samsung_Flash_Memory.pdf)



# UFS (Universal Flash Storage)
UFS = SATA High Speed + SCSI Standardization + eMMC Low Power

JEDEC defines UFS as the next generation mobile storage spec

![001](/img/2016-03-07-eMMC-UFS-About-UFS-1/001.JPG)
![002](/img/2016-03-07-eMMC-UFS-About-UFS-1/002.JPG)
![003](/img/2016-03-07-eMMC-UFS-About-UFS-1/003.JPG)

#### UFS Serial Interface

- the demand for speed and cost has led to parallel communication links becoming deprecated in favor of serial links.
- Speed:
  - Clock skew reduces the speed of every link.
  - Crosstalk creates interference between the parallel lines
- Cost: The decreasing cost of integrated circuits

![004](/img/2016-03-07-eMMC-UFS-About-UFS-1/004.JPG)

#### UFS AsyncCommand & Command Queuing

- Set it and forget it
- Optimal for multi processing
- Support multiple CMD queuing Maximize parallel programming
- Better throughput through better NAND utilization

![005](/img/2016-03-07-eMMC-UFS-About-UFS-1/005.JPG)

- Re-Ordering.
  - Command queue execution sequence can be changed by considering NAND interleaving
  - Numberof active NAND chips per time is improved
  - Suitable for UFS because UFS protocol is a multi-thread, asynchronous protocol
  
#### UFS has better features than eMMC

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

#### UFS : Simple PCB routing and cost save

![006](/img/2016-03-07-eMMC-UFS-About-UFS-1/006.JPG)
![010](/img/2016-03-07-eMMC-UFS-About-UFS-1/010.JPG)
![011](/img/2016-03-07-eMMC-UFS-About-UFS-1/011.JPG)
![007](/img/2016-03-07-eMMC-UFS-About-UFS-1/007.JPG)

#### Functional Comparison for HW Perspective

Item | eMMC5.0 | UFS2.0
---- | ----- | ----
HostI/F Speed | DDR400Mhz | 3Ghzx2Lane(6Ghz)
HostSignal Type | CMOS | LVDS
I/Oswing Level | 1.8V | 240mV
Comm.Type | HalfDuplex | FullDuplex
I/OError Detection | CRC16/512Byte | CRC16/272Byte
BufferControl | Busysignal | Uniprosupport, RTT
Sector Size | 512 Byte | 4096 Byte (RPMB512Byte)
RPMB | O | O
#Lun | 4 | 8 
Boot Partition | O | O
Fast Boot |O | O
Command Queue | X | O 
Concurrent Ops. | X | O
Secure Trim/Erase | O | O 
Other eMMC features | O | O
Command Protocol | eMMC | SCSI

#### New feature list for each standard ver

![008](/img/2016-03-07-eMMC-UFS-About-UFS-1/008.JPG)

#### Memory I/F Trend on Mobile Application

![008](/img/2016-03-07-eMMC-UFS-About-UFS-1/008.JPG)