---
layout: post
title:  "eMMC UFS Issues 17"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

## Component Feature
- 
- Controller : 
- Hy

## Failure Symptom
- No power-on on smart phone.
- infinite loop booting

## Possible Error Type
- NAND Level : bit flip error due to particle or fab error 
- FW Level : bit flip from FW error
- emmc internal SRAM Level : bit flip from SRAM unstability

## Conclusion after inspection of bit flip
- The NAND level and FW Level have on doubt.
- The cause suspicion is that the bit flip was casused from SRAM data failure , and the data was written to NAND , the wrong data was transferd at booting time.

## What is the soft error ? 
- is bit flip
- but  if rewrite , the error can be recovered.

Cause | Description 
---- | -----
A. Alpha particles from package | caused by radioactive materials Trace within package
B. Cosmic rays creating energetic neutrons and protons | caused by high energy from Atmospheric environment
C. Thermal | The energy stored in the cell is lost over time, as the temperature accelerates and the original data is transformed
D. Random Noise or Signal Integrity(Include Current Spike) | Random noise and signal integration problem wih power and signal
 | can occurs when the voltage is dropped to under operation voltage Momentarily
 
<img src="/img/2017-01-20-eMMC-UFS-Issues-17/001.JPG" width="300" /><img src="/img/2017-01-20-eMMC-UFS-Issues-17/002.JPG" width="300" /><img src="/img/2017-01-20-eMMC-UFS-Issues-17/003.JPG" width="300" /><img src="/img/2017-01-20-eMMC-UFS-Issues-17/004.JPG" width="300" />

## Instant Voltage Drop on eMMC
- A potent suspect factor
- the evidence 

<img src="/img/2017-01-20-eMMC-UFS-Issues-17/005.JPG" width="400" />

- VCCQ ( 1.2V ) voltage was dropped momentarily between 30nS and 50nS 

## How to prevent the bit flip on SRAM of eMMC 

- install a voltage regulator in front of VCCQ
- detect the instant voltage drop, and then reset system.
- checksum algorithm applying to SRAM

1.In Normal Operation
- Critical management tables are being verified by checksum algorithm
- Before any update or flush to NAND, checksum is calculated and verified

2.In Sleep Mode(cmd5 and AutoSleep )
- While entering and exiting sleep, RAM refresh algorithm is activated
- Read Data --> Detect bit flip --> Recover if needed

![006](/img/2017-01-20-eMMC-UFS-Issues-17/006.JPG)

- Integrity of data is assured during data flow within the ASIC
- No performace impact
 
