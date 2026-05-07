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
source-wordcount: '136'
ht-degree: 24%

---

# 推奨事項{#recommendations}



Adobe Campaignは、OLTP （highly transactional system）の略です。 つまり、基礎となるデータベースが頻繁に更新され、時間の経過とともにパフォーマンスが低下します。 このような問題を回避するには、定期的なデータベースのメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的に維持されなければ最適なパフォーマンスを発揮しません。 一部のRDBMSが提供する自動メンテナンスは十分ではなく、リレーショナルデータベースのトランザクション管理システムのように、詳細なメンテナンスに代わるものではありません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の責任です。問題が発生した場合は、最初に連絡を取る必要があります。
