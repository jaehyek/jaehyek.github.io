---
layout: post
title:  "eMMC & UFS FTL (3)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS FTL
author: Jaehyek
---

# FTL Functions

### Wear Leveling
- Wear leveling software monitors Flash erase block cycling and guarantees that all erase block are cycled about the same number of times.
- Some files are seldom changed, while others may be changed frequently. If all files were updated at the same frequency, wear leveling would not be necessary.
![001](/img/2016-12-07-eMMC-UFS-FTL-3/001.JPG)

### Handling Device Error
- Handing Bad Block for NAND
 - NAND permits 1-2% factory or run time bad blocks
 - BD tract this information through marking to the head of block or separate table
 - BD have to have strategy to decide run-time bad block when read/write/erase error happens
 
- Handling Bit error for NAND
 - One or a few bit error happens rarely in NAND.
 - Error collection code can allow the area to live instead of throw it away by marking Bad block

### Power Loss Problem
- Power loss break BD’s integrity in various way
 - Crash BD and make BD be disable to mount
 - Point wrong physical block for a virtual sector
![002](/img/2016-12-07-eMMC-UFS-FTL-3/002.JPG) 

- Lost Data Case

![003](/img/2016-12-07-eMMC-UFS-FTL-3/003.JPG) 

 

