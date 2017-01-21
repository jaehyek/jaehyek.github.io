---
layout: post
title:  "eMMC & UFS About UFS (2)"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS About
author: Jaehyek
---

## UFS Architecture

![001](/img/2016-03-07-eMMC-UFS-About-UFS-2/001.JPG)

## UFS Protocol Layer

![002](/img/2016-03-07-eMMC-UFS-About-UFS-2/002.JPG)

## UFS Architecture 2 

![003](/img/2016-03-07-eMMC-UFS-About-UFS-2/003.JPG)

## M-PHY 

Each 1LANE
- Normal Speed : 
  - PWM-G0 ~ PWM-G7 : PWM G1 : 3 ~ 9Mbps
- HS-G1 ~ HS-G3( High Speed )
  - HS-G1 : (1.25Gbps or 1.45Gbps)
  - HS-G2 : (2.5Gbps or 2.9Gbps)
  - HG-G3 : (5Gbps or 5.8Gbps)
  
- TYPE I : PWM Signaling in UFS 1.0
- TYPE II : system Clock Reference(NRZ Signaling)

- UFS 1.0(currently) : 
  - 2.9Gbps(HS-G2) & 1.45Gbps(HS-G1) 

![004](/img/2016-03-07-eMMC-UFS-About-UFS-2/004.JPG)

- Extensible by lane increase in pairs
- Each lane’s speed is 2.9Gbps(HS-G2).
  - So, ideal bi-directional speed is double of this
- Interface of card type UFS is same as M-PHY of embedded UFS. So, host side implementations (HW, SW) have no difference

## UNIPRO ( Unified Protocol ) 

- Optimized
  - For mobile use cases & multiple applications
  - Low power & small battery-powered systems
  
- Enables minimized/extendable implementations
- Reliability with error detection and correction via retransmission simplifies protocol design
- Optimally uses MIPI’s PHY technologies
  - Allows aggressive power optimization
  - Allows for bandwidth scaling options
- Formal UniPro SDL model available
- UniPro testing specification available

![005](/img/2016-03-07-eMMC-UFS-About-UFS-2/005.JPG)

## UTP
 
- highestHW Layer
- SLOT: HW Resource for Command Acceptance
- 32 CMD Slots, 8 Task Slot, 1 Query Slot Each Slot has it’s own DESC.(Description of operation)

![006](/img/2016-03-07-eMMC-UFS-About-UFS-2/006.JPG)

## Hardware vs. Software

![007](/img/2016-03-07-eMMC-UFS-About-UFS-2/007.JPG)

## UFS Standardization

![008](/img/2016-03-07-eMMC-UFS-About-UFS-2/008.JPG)

## UFS UPIU

![009](/img/2016-03-07-eMMC-UFS-About-UFS-2/009.JPG)
![010](/img/2016-03-07-eMMC-UFS-About-UFS-2/010.JPG)

## UFS UPIU Transaction Type 
![011](/img/2016-03-07-eMMC-UFS-About-UFS-2/011.JPG)

## UFS Command Flow 
![012](/img/2016-03-07-eMMC-UFS-About-UFS-2/012.JPG)

100~104 Sector Read 
![013-0](/img/2016-03-07-eMMC-UFS-About-UFS-2/013-0.JPG)
![013](/img/2016-03-07-eMMC-UFS-About-UFS-2/013.JPG)
![014](/img/2016-03-07-eMMC-UFS-About-UFS-2/014.JPG)

## Read Operation Flow 
![015](/img/2016-03-07-eMMC-UFS-About-UFS-2/015.JPG)

## Write Operation Flow 
![016](/img/2016-03-07-eMMC-UFS-About-UFS-2/016.JPG)
![017](/img/2016-03-07-eMMC-UFS-About-UFS-2/017.JPG)

## SCSI Command 

ScsiCommand Set supported by UFS is based on UFS native commands and Scsiprimary commands spec(SPC-4/SBC-3).

Commands (CDB Size) | Description | DATA IN UPIU | DATA OUT UPIU
---- |-----|-----|----
**TEST UNIT READ(6)** | Test if device is ready (not for a self-test) | X | X
**Inquiry(6)** | Report device information -type, manufacture, etc | a single Data In UPIU(36byte) | X 
**Request Sense(6)** | Report sense data -current status of device | a single Data In UPIU(18byte) | X
**Read Capacity(10)** | Report medium capacity and block sizecan be issued per Logical Unit | a single Data In UPIU(8byte) | X
**Start Stop Unit(6)** | Change power condition or load or eject medium | X | X
**Read(10)** | Transfer data from medium to host | a series of Data In UPIU's | X
**Write(10)** | Transfer data from host to medium | Ready To Transfer UPIU | a Data OUT UPIU per RTT
**Read Buffer(10)** | Read microcode and other data and tunneling | a series of Data In UPIU's | X
**Write Buffer(10)** | Transfer microcode and other data and tunnelling | Ready To Transfer UPIU | a Data OUT UPIU per RTT
**Mode Select(10)** | Set parameter , modes, etc | Ready To Transfer UPIU | a Data OUT UPIU per RTT
**Mode Sense(10)** | Report parameters and other device Information -geometry, other | a series of Data In UPIU's | X
**Report LUNS(12)** | Report the accessible logical unit inventory | one or more Data IN UPIU's (Most likely one data in UPIU) (8byte+8 x n) (n = LUN) | X
**Verify(10)** | Verify medium data is same as transferred dataTo determine if specific LBA's are accessible | X | X
**Format Unit(6)** | Format medium into logical blocks, manage medium and defects | Ready To Transfer UPIU | a Data Out UPIU containing the unmber of bytes
**Send Diagnostic(6)** | Perform diagnostic operations on LU or device | Ready To Transfer UPIU | a Data Out UPIU containing the unmber of bytes
**Synchronize Cache(10)** | Recording most recent device data to medium | X | X

## SCSI Command & Operation

- Scsicommands operation by Command Flag Type
- No Data (Test Unit Ready, Start Stop Unit, Verify)
![019](/img/2016-03-07-eMMC-UFS-About-UFS-2/019.JPG)
![020](/img/2016-03-07-eMMC-UFS-About-UFS-2/020.JPG)

- Data from Device (Inquiry, Read6, Request Sense, Read Capacity, Mode Sense, Report LUN)
![021](/img/2016-03-07-eMMC-UFS-About-UFS-2/021.JPG)

- Data to Device (Write6, Mode Select, Unmap, Format Unit)
![022](/img/2016-03-07-eMMC-UFS-About-UFS-2/022.JPG)

## Descriptor & Attribute
- Descriptor : General Configuration for Device-level
- Attribute : Frequently Configurable Range Value
- Flag : Frequently ConfigurableBOOL Value

![023](/img/2016-03-07-eMMC-UFS-About-UFS-2/023.JPG)

#### Descriptor
![024](/img/2016-03-07-eMMC-UFS-About-UFS-2/024.JPG)

![025](/img/2016-03-07-eMMC-UFS-About-UFS-2/025.JPG)
![026](/img/2016-03-07-eMMC-UFS-About-UFS-2/026.JPG)
![027](/img/2016-03-07-eMMC-UFS-About-UFS-2/027.JPG)

#### Attribute & Flag
![028](/img/2016-03-07-eMMC-UFS-About-UFS-2/028.JPG)
