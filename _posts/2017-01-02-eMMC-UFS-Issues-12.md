---
layout: post
title:  "eMMC UFS Issues 12"
categories: eMMC-UFS
comments: true
tags:  eMMC UFS Issues
author: Jaehyek
---

# Component Feature
- eMMC5.1
- Controller : 
- Qual

# Failure Symptom
- CodeAurora Released Patch for Kernel msm-3.18
- Reference : http://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/drivers/mmc?h=LV.HB.1.1.2-09110-8x96.0&id=e1b3c352dbf1c132a24dbbd176339ceec5d4862c

# Root Cause
- At Qualcomm chip emmc 5.1 
- From kernel 3.18 , Auto BKOPS enable bit is saved to system block ( RPMB )
- eMMC Driver write the BKOPS enable bit to EXT_CSD register when suspen/resume 
- Frequent suspend/resume makes the frequent writing to system block, and then caused EOL ( end of life )
- The patch prevent the  enable/disable function of BKOPS when suspen/resume 

![001](/img/2017-01-02-eMMC-UFS-Issues-12/001.JPG)

at  drivers/mmc/core/mmc.c
~~~
diff --git a/drivers/mmc/core/mmc.c b/drivers/mmc/core/mmc.c
index 73c17db..f90e297 100644
--- a/drivers/mmc/core/mmc.c
+++ b/drivers/mmc/core/mmc.c
@@ -2378,12 +2378,6 @@ static int _mmc_suspend(struct mmc_host *host, bool is_suspend)
 			goto out;
 	}
 
-	if (mmc_card_doing_auto_bkops(host->card)) {
-		err = mmc_set_auto_bkops(host->card, false);
-		if (err)
-			goto out;
-	}
-
 	err = mmc_flush_cache(host->card);
 	if (err)
 		goto out;
@@ -2463,9 +2457,6 @@ static int mmc_partial_init(struct mmc_host *host)
 	pr_debug("%s: %s: reading and comparing ext_csd successful\n",
 		mmc_hostname(host), __func__);
 
-	if (mmc_card_support_auto_bkops(host->card))
-		(void)mmc_set_auto_bkops(host->card, true);
-
 	if (card->ext_csd.cmdq_support && (card->host->caps2 &
 					   MMC_CAP2_CMD_QUEUE)) {
 		err = mmc_select_cmdq(card);
~~~


# Mechanism of  BKOPS Operation
![002](/img/2017-01-02-eMMC-UFS-Issues-12/002.JPG)

# Failure Mode estimation of this issue
[AUTO_EN Update usage @ A Customer system] (Chipset : MSM8953 / Kernel version : 3.18.24)
In worst case, this issue makes the emmc life to be 1 year
![003](/img/2017-01-02-eMMC-UFS-Issues-12/003.JPG)