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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2a11a73b0679c0a65dc10f71869bf2a6c6efc008

---


# 推奨事項{#recommendations}

Adobe Campaignは、高度なトランザクション処理を行うシステム（OLTPデータベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このような問題を回避するには、定期的なデータベースメンテナンスが必要です。

>[!CAUTION]
>
>データベースは、定期的に保守される場合にのみ最適に実行されます。 一部のRDBMSで提供される自動メンテナンスは、リレーショナル・データベースのトランザクション管理システムとは異なり、十分ではなく、詳細なメンテナンスを置き換えることができません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の応答性を表します。問題が発生した場合は、最初に連絡する必要があります。

