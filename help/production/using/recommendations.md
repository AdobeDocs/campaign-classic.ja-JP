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
TQID: https://experienceleague.adobe.com/hz0wmjq8MEpmen-C30F0tHt5-sRXjQAJ6vaie3hjfAo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 136
ht-degree: 24%

---

# 推奨事項{#recommendations}



Adobe Campaignは、OLTP （highly transactional system）の略です。 つまり、基礎となるデータベースが頻繁に更新され、時間の経過とともにパフォーマンスが低下します。 このような問題を回避するには、定期的なデータベースのメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的に維持されなければ最適なパフォーマンスを発揮しません。 一部のRDBMSが提供する自動メンテナンスは十分ではなく、リレーショナルデータベースのトランザクション管理システムのように、詳細なメンテナンスに代わるものではありません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の責任です。問題が発生した場合は、最初に連絡を取る必要があります。
