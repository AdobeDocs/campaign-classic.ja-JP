---
title: 推奨事項
seo-title: 推奨事項
description: 推奨事項
seo-description: null
page-status-flag: never-activated
uuid: d898fe6d-7627-405f-b2bc-b17bf1dc9e96
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: database-maintenance
discoiquuid: a31c5c9f-503f-4b55-8409-34d4addbd581
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 3%

---


# 推奨事項{#recommendations}

Adobe Campaignは、トランザクションの多いシステム（OLTPデータベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このような問題を回避するには、定期的なデータベースメンテナンスが必要です。

>[!CAUTION]
>
>データベースは、定期的に保守されている場合にのみ最適に実行されます。 一部のRDBMSで提供される自動メンテナンスは不十分で、リレーショナル・データベースのトランザクション管理システムの場合と同様に、詳細なメンテナンスを置き換えることができません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の応答性です。問題が発生した場合は最初に連絡する必要があります。

