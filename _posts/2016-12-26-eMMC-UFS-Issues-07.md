---
layout: post
title:  "eMMC UFS Issues 07"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- 32GB UFS 2.0
- Controller : 
- Hy

# Failure Symptom
- UFS init fail

# Failure procedure
- When  the Read Reclaim for Supper Block was triggered and SPO was occured
- The history log was not remained atomically 
![001](/img/2016-12-26-eMMC-UFS-Issues-07/001.JPG)

# Fixed to work after SPO
![002](/img/2016-12-26-eMMC-UFS-Issues-07/002.JPG)