---
title: v6.1 の復元
seo-title: v6.1 の復元
description: v6.1 の復元
seo-description: null
page-status-flag: never-activated
uuid: 3fb71b6f-4d70-4814-a885-4d414a542eca
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: e510482c-a56d-4254-90f8-19bd5c545e30
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 9%

---


# v6.1 の復元{#restoring-v}

v7からv6.1を復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Adobe Campaignv6.back **Adobe Campaign(Linuxでは** nl6.back **)を回復し、フォルダ名を** v6に変更し(Linuxでは ******** nl6)、元の場所に戻します。
1. リスンポートを再割り当てしてIISを再設定し、Adobe Campaignv6.1の統合をIIS Webサイトレベルで再確立します。
1. Adobe Campaignv7サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv6.1サービスを再起動します。

