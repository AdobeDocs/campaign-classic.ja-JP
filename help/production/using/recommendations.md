---
product: campaign
title: 推奨事項
description: 推奨事項
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: e458f6cb-f6d1-4688-9f6d-2a27a2f90829
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 2%

---

# 推奨事項{#recommendations}

![](../../assets/v7-only.svg)

Adobe Campaignは、高トランザクションシステム（OLTP データベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このタイプの問題を回避するには、データベースの定期的なメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的にメンテナンスされている場合にのみ最適に実行されます。 一部の RDBMS で提供される自動メンテナンスは十分ではなく、リレーショナルデータベーストランザクション管理システムと同様に、詳細なメンテナンスに代わるものではありません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の責任です。問題が発生した場合は最初に連絡する必要があります。
