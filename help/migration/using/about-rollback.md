---
product: campaign
title: 以前のバージョンへのロールバック
description: 以前のバージョンにロールバックする方法を説明します
feature: Upgrade
audience: migration
content-type: reference
topic-tags: rollback
hide: true
hidefromtoc: true
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 以前のバージョンへのロールバック{#about-rollback}



移行後に問題が発生した場合は、以前のバージョンの Campaign にロールバックする必要が生じる場合があります。

ロールバックの手順は、Campaign の初期バージョンによって異なります。

v7 から v6.1 を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、リストアします。
1. **Adobe Campaign v6.back** フォルダー（Linux の場合は **nl6.back** を復元し、**Adobe Campaign v6** （Linux の場合は **nl6**）に名前を変更して元の場所に復元します。
1. リッスンポートを再割り当てして IIS を再設定し、IIS Web サイトレベルでAdobe Campaign v6.1 の統合を再確立します。
1. Adobe Campaign v7 サービスを停止します。
1. IIS を再起動します。
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