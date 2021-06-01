---
product: campaign
title: 以前のバージョンにロールバックする
description: 以前のバージョンにロールバックする方法を説明します
audience: migration
content-type: reference
topic-tags: rollback
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 以前のバージョンにロールバック{#about-rollback}

移行後、問題が発生した場合は、以前のバージョンのCampaignにロールバックする必要が生じる可能性があります。

ロールバック手順は、Campaignの最初のバージョンによって異なります。

## v6.1 の復元

v7からv6.1を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Adobe Campaign v6.back**&#x200B;フォルダー（Linuxの場合は&#x200B;**nl6.back**）を回復し、名前を&#x200B;**Adobe Campaign v6**（Linuxの場合は&#x200B;**nl6**）に変更して、元の場所に復元します。
1. IIS WebサイトレベルでAdobe Campaign v6.1の統合を再確立するために、リスンポートを再割り当てしてIISを再設定します。
1. Adobe Campaign v7サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v6.1サービスを再起動します。

## Campaign v6.02への復元

v7からv6.02を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Neolane v6.back**&#x200B;フォルダー（Linuxの場合は&#x200B;**nl6.back**）を回復し、名前を&#x200B;**Neolane v6**（Linuxの場合は&#x200B;**nl6**）に変更して、元の場所に戻します。
1. IIS WebサイトレベルでAdobe Campaign v6.02の統合を再確立するために、リスンポートを再割り当てしてIISを再設定します。
1. Adobe Campaign v6.1サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v6.02サービスを再起動します。

## Campaign v5.11への復元

v7からv5.11を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Neolane v5.back**&#x200B;フォルダー（Linuxの場合は&#x200B;**nl5.back**）を回復し、名前を&#x200B;**Neolane v5**（Linuxの場合は&#x200B;**nl5**）に変更して、元の場所に戻します。
1. リスンポートを再割り当てしてIISを再設定し、IIS WebサイトレベルでNeolane v5の統合を再確立します。
1. Adobe Campaign v7サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v5サービスを再起動します。
