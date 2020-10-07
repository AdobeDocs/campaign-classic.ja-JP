---
title: v6.02 の復元
seo-title: v6.02 の復元
description: v6.02 の復元
seo-description: null
page-status-flag: never-activated
uuid: df21209b-4825-42fa-a303-f383f872abb5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: 4f65ba19-e9f0-4425-b640-f27c61394859
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 9%

---


# v6.02 の復元{#restoring-v}

v7からv6.02を復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Neolane v6.back **フォルダー(Linuxでは** nl6.back **)を回復し、** Neolane v6 **.backフォルダー(Linuxでは** nl6.back **** )に名前を変更し、元の場所に戻します。
1. リスンポートを再割り当てしてIIS WebサイトレベルでAdobe Campaignv6.02の統合を再確立し、IISを再設定します。
1. Adobe Campaignv6.1サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv6.02サービスを再起動します。

