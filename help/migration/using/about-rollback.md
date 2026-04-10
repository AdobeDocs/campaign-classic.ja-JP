---
product: campaign
title: 前のバージョンにロールバック
description: 以前のバージョンにロールバックする方法について説明します
feature: Upgrade
audience: migration
content-type: reference
topic-tags: rollback
hide: true
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: 76f483dcda9f8a5ed93355d68bb1d1a589d55722
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 前のバージョンにロールバック{#about-rollback}



移行後に問題が発生した場合は、以前のバージョンのCampaignにロールバックする必要がある場合があります。

ロールバック手順は、Campaignの初期バージョンによって異なります。

v6.1をv7から復元する手順は次のとおりです。

1. データベースのバックアップを復元し、復元します。
1. **Adobe Campaign v6.back** フォルダー（**nl6.back** Linux）を復元し、名前を&#x200B;**Adobe Campaign v6** （**nl6** Linux）に変更して、元の場所に復元します。
1. IIS Web サイト レベルでのAdobe Campaign v6.1の統合を再確立するために、リッスン ポートを再割り当てすることにより、IISを再構成します。
1. Adobe Campaign v7 サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v6.1 サービスを再起動します。

<!--
	
## Restore to Campaign v6.02

Here is the procedure to restore a v6.02 from a v7.

1. Recover the backup of the database and restore it.
1. Recover the **Neolane v6.back** folder (**nl6.back** in Linux), rename it to **Neolane v6** (**nl6** in Linux) and restore it to its original location.
1. Re-configure IIS by re-assigning the listen ports to re-establish the integration of Adobe Campaign v6.02 at IIS Website level.
1. Stop the Adobe Campaign v6.1 service.
1. Re-start IIS.
1. Restart the Adobe Campaign v6.02 service.

## Restore to Campaign v5.11

Here is the procedure to restore a v5.11 from a v7.

1. Recover the backup of the database and restore it.
1. Recover the **Neolane v5.back** folder (**nl5.back** in Linux), rename it to **Neolane v5** (**nl5** in Linux) and restore it to its original location.
1. Re-configure IIS by re-assigning the listen ports to re-establish the integration of Neolane v5 at IIS Website level.
1. Stop the Adobe Campaign v7 service.
1. Re-start IIS.
1. Re-start the Adobe Campaign v5 service.

-->