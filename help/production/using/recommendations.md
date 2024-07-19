---
product: campaign
title: 推奨事項
description: 推奨事項
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: e458f6cb-f6d1-4688-9f6d-2a27a2f90829
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---

# 推奨事項{#recommendations}



Adobe Campaignは、トランザクションの多いシステム（OLTP データベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 この種の問題を回避するには、定期的なデータベースのメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的に維持する場合にのみ最適に実行されます。 一部の RDBMS が提供する自動メンテナンスでは、リレーショナル・データベースのトランザクション管理システムと同様に、十分ではなく、詳細なメンテナンスに取って代わるものではありません。
>  
>このドキュメントで説明されている手順は推奨事項です。 メンテナンス計画は、データベース管理者の責任であり、問題が発生した場合の最初の連絡先となる必要があります。
