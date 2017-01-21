---
layout: post
title:  "eMMC & UFS About UFS (3)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS About
author: Jaehyek
---

## UFS HCI ( HOST Controller Interface )

![001](/img/2016-03-07-eMMC-UFS-About-UFS-3/001.JPG)

## HCI Register

![002](/img/2016-03-07-eMMC-UFS-About-UFS-3/002.JPG)
![003](/img/2016-03-07-eMMC-UFS-About-UFS-3/003.JPG)

## UTP Transfer Request

![004](/img/2016-03-07-eMMC-UFS-About-UFS-3/004.JPG)

## UTP Transfer Request Completion

![005](/img/2016-03-07-eMMC-UFS-About-UFS-3/005.JPG)

## Host Controller link startup

![006](/img/2016-03-07-eMMC-UFS-About-UFS-3/006.JPG)

## Host Power Mode Change

![007](/img/2016-03-07-eMMC-UFS-About-UFS-3/007.JPG)

## UFS Device

#### Device E2E Interface

![008](/img/2016-03-07-eMMC-UFS-About-UFS-3/008.JPG)

#### Logical Unit
- LU : Externally addressable, independent, processing entity
- Device contains 1 or Max 8 Normal logical units & 4 Well-known LU
- A Logical unit contains : 
  - DEVICE SERVER : Processing SCSI Commands
  - TASK MANAGER : Performs Task management Functions
  - TASK SET : A Conceptual Group of Commands
  
![009](/img/2016-03-07-eMMC-UFS-About-UFS-3/009.JPG)

#### LU Configuration

![010](/img/2016-03-07-eMMC-UFS-About-UFS-3/010.JPG)
![010-1](/img/2016-03-07-eMMC-UFS-About-UFS-3/010-1.JPG)

#### LU Configuration : description

![011](/img/2016-03-07-eMMC-UFS-About-UFS-3/011.JPG)

#### Higher Priority LU

![012](/img/2016-03-07-eMMC-UFS-About-UFS-3/012.JPG)
![013](/img/2016-03-07-eMMC-UFS-About-UFS-3/013.JPG)

#### Boot Sequence

![014](/img/2016-03-07-eMMC-UFS-About-UFS-3/014.JPG)

#### SCSI Command & Operation (Unmap)

![015](/img/2016-03-07-eMMC-UFS-About-UFS-3/015.JPG)

#### Write Protection

![016](/img/2016-03-07-eMMC-UFS-About-UFS-3/016.JPG)

