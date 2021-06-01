---
product: campaign
title: 推奨事項
description: 推奨事項
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: e458f6cb-f6d1-4688-9f6d-2a27a2f90829
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 2%

---

# 推奨事項{#recommendations}

Adobe Campaignは、OLTPデータベース（高トランザクション・システム）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このタイプの問題を回避するには、通常のデータベースメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的にメンテナンスされている場合にのみ最適に実行されます。 一部のRDBMSで提供される自動メンテナンスは十分ではなく、リレーショナル・データベース・トランザクション管理システムの場合とは異なり、詳細なメンテナンスに置き換えられません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の応答性です。問題が発生した場合は、最初に連絡する必要があります。
