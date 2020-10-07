---
title: v5.11 の復元
seo-title: v5.11 の復元
description: v5.11 の復元
seo-description: null
page-status-flag: never-activated
uuid: 4480c97c-5845-483c-a17b-644f05783b4e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: ef778333-8e50-402b-9a69-78ac94497c67
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 9%

---


# v5.11 の復元{#restoring-v}

v5.11をv7から復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Neolane v5.back **フォルダ(Linuxでは** nl5.back **)を回復し、名前を** Neolane v5 **(Linuxでは****** nl5)に変更し、元の場所に戻します。
1. リスンポートを再割り当てしてIIS WebサイトレベルでNeolane v5の統合を再確立し、IISを再設定します。
1. Adobe Campaignv7サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv5サービスを再開始します。

