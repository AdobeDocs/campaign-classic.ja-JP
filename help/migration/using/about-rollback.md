---
product: campaign
title: 以前のバージョンにロールバック
description: 以前のバージョンにロールバックする方法を説明します。
feature: Upgrade
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: migration
content-type: reference
topic-tags: rollback
hide: true
hidefromtoc: true
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 5%

---

# 以前のバージョンにロールバック{#about-rollback}



移行後、問題が発生した場合は、以前のバージョンの Campaign へのロールバックが必要になる場合があります。

ロールバック手順は、Campaign の最初のバージョンに応じて異なります。

v7 から v6.1 を復元する手順を次に示します。

1. データベースのバックアップを復元し、復元します。
1. 次を回復します。 **Adobe Campaign v6.back** フォルダー (**nl6.back** （Linux の場合）、名前をに変更します。 **Adobe Campaign v6** (**nl6** Linux の場合 )、を元の場所に戻します。
1. IIS Web サイトレベルでAdobe Campaign v6.1 の統合を再確立するために、リスンポートを再割り当てして IIS を再設定します。
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