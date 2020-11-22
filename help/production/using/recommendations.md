---
solution: Campaign Classic
product: campaign
title: 推奨事項
description: 推奨事項
audience: production
content-type: reference
topic-tags: database-maintenance
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 2%

---


# 推奨事項{#recommendations}

Adobe Campaignは、トランザクションの多いシステム（OLTPデータベース）です。 つまり、基になるデータベースは頻繁に更新され、時間の経過と共にパフォーマンスが低下します。 このような問題を回避するには、定期的なデータベースメンテナンスが必要です。

>[!IMPORTANT]
>
>データベースは、定期的に保守されている場合にのみ最適に実行されます。 一部のRDBMSで提供される自動メンテナンスは不十分で、リレーショナル・データベースのトランザクション管理システムの場合と同様に、詳細なメンテナンスを置き換えることができません。
>  
>このドキュメントで説明する手順は、推奨事項です。 メンテナンスプランは、データベース管理者の応答性です。問題が発生した場合は最初に連絡する必要があります。
