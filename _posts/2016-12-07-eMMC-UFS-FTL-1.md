---
layout: post
title:  "eMMC & UFS FTL (1)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS FTL
author: Jaehyek
---

# FTL (Flash Translation Layer)

### Flash’s Limitation
- No overwrite without Erase
- Big erase block : ex. 2MB
- Factory Bad Block and Run time Bad Block
- Run time bit error
- Limited Lifetime : ex) Erase 5K for an Erase Block

### FTL’s Roles
- Flash Translation Layer : mapping virtual sector to physical block
- Garbage Collection
- Power Loss Recovery
- Error Correction
- Bad Block Management
- Wear leveling

### Address Remapping
- Address mapping table
- Trying to update data of (Sector #3045) stored NAND(Block #125, Page #29)
![001](/img/2016-12-07-eMMC-UFS-FTL-1/001.JPG)

### Sector Mapping
LSN: Logical Sector Number
PSN : Physical Sector Number
![002](/img/2016-12-07-eMMC-UFS-FTL-1/002.JPG)

### Block Mapping
LBN: Logical Block Number
PBN : Physical Block Number
![003](/img/2016-12-07-eMMC-UFS-FTL-1/003.JPG)

### Hybrid Mapping
![004](/img/2016-12-07-eMMC-UFS-FTL-1/004.JPG)