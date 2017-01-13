---
layout: post
title:  "eMMC UFS Issues 14"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 
- Controller : 
- Mi

# Failure Symptom
- Smart Phone hang-up

# Root Cause
- Vt distribution shows the UECC block has been double programmed in MLC mode.

# Cause procedure
After reviewing the firmware structure, the following scenario of event sequence has been identified as suspected failure sequence <br/>  
1. During power up init, firmware selects the block to use, for example the BLK-A never used before and sets the dirty bit='1' in SRAM
2. Firmware enters suspend mode (auto standby) after few ms. Some SRAM including dirty bit of BLK-A will be turn off during suspend mode.
3. Write command triggers the device awakes from suspend mode and firmware uses  the BLK-A without erase it. The dirty bit "i" and P/E of BLK-A will be updated into a system block when the write operation is completed
4. If power loss occurs during write BLK-A in step 3, the information related to the BLK-A will be lost. In the next power cycle, due to FW bug, BLK-A is again recognized as never used block and by repeating step 1-3, the BLK-A is used without erase, thus double program can occur.

Note : FW management of dirty bit of never used NAND block ( P/W=1) <br/> 
- To avoid the FW perform unnecessary erase of a never used NAND block, there is a dirty bit flag. When the dirty bit is set to "1", erase is needed before program. on the contrary, if dirty bit is clean, no need to erase before program.
- This bit is no more used on the NAND block erased at least one time (P/E>=2)


# Conclusions:
A firmwar issue is confirmed , the firmware issue will induce NAND block double programmed after power loss.

As this is productin failure observed after 300K units processed, Micron considers it as singular case where uncontrolled power cuts occur in line ( 11 times of power loss )

At end user side, by assuming 3/5GB x day transferred in the early usage of the phone, it is expected that within few days all NAND blocks of the device will be written once and this issue will not be triggered after that.
