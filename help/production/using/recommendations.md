---
product: campaign
title: 推奨事項
description: 推奨事項
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: e458f6cb-f6d1-4688-9f6d-2a27a2f90829
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 2%

---

# 推奨事項{#recommendations}



Adobe Campaignは、高トランザクションシステム（OLTP データベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このタイプの問題を回避するには、データベースの定期的なメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的にメンテナンスされている場合にのみ最適に実行されます。 一部の RDBMS で提供される自動メンテナンスは十分ではなく、リレーショナルデータベーストランザクション管理システムと同様に、詳細なメンテナンスに代わるものではありません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の責任です。問題が発生した場合は最初に連絡する必要があります。
