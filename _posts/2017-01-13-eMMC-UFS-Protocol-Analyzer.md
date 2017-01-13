---
layout: post
title:  "eMMC Protocol Analyzer"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Protocol Analyzer
author: Jaehyek
---

# eMMC Protocol Analyzer Setup
![001](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/001.JPG)

# [SGDK330B information]

SGDK330B was newly lined up to analyzer (June 2015) <br/>
SGDK330B Main POD has 1GB memory on board, so it has following functions <br/>

- SGDK330B can save all of protocol information of HS400 mode.
- On the other hand, SGDK330A cannot save all of protocol information of HS400 mode.
- SGDK330A can save only 256Byte (half of one sector) information of HS400 mode.
- Maximum LOG size of SGDK330B is 1GB

Architecture of SGDK330B is the same as SGDK330A. <br/>
All of Mini POD can be used for both SGDK330A and SGDK330B. <br/>
Differences between SGDK330A and SGDK330B are the items which are related to 1GB on board. <br/>

# Mechanism
![002](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/002.JPG)
![003](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/003.JPG)

All of data (DATA[7:0]) are connected case
![004](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/004.JPG)

Only DATA[0] is connected case
![005](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/005.JPG)

# Mini POD for eMMC/SDIO wire type]

![006](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/006.JPG)

# CMD8 (SEND_EXT_CSD)]
![007](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/007.JPG)

# Mini POD
![008](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/008.JPG)
![009](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/009.JPG)
![010](/img/2017-01-13-eMMC-UFS-Protocol-Analyzer/010.JPG)



