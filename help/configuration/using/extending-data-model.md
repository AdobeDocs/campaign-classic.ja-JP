---
title: Adobe Campaign Classic Recipientテーブルの使用
description: Adobe Campaign Classicでデータモデルをデザインする際に、あらかじめ用意されている受信者テーブルを使用する方法を説明します。
page-status-flag: never-activated
uuid: faddde15-59a1-4d2c-8303-5b3e470a0c51
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: 5957b39e-c2c6-40a2-b81a-656e9ff7989c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 65affa58a66090c3bffc837fdbd85aa46338bd3e

---


# データモデルの拡張{#extending-data-model}

Adobe Campaignを使用する場合は、デフォルトのデータモデルを評価して、マーケティングデータの保存に最適なテーブルを確認する必要があります。

関連する場合は、この節で説明するように、あらかじめ用意されているフィールドでデフォルトの受信者テーブルを使用で [きます](../../configuration/using/default-recipient-table.md)。

必要に応じて、次の2つのメカニズムを使用して拡張できます。

* 既存のテーブルを新しいフィールドで拡張します。 例えば、新しい「忠誠度」フィールドを「受信者」テーブルに追加できます。
* 新しいテーブル（例えば、「購入」テーブル）を作成し、データベースの各プロファイルによる購入をすべて一覧表示して、「受信者」テーブルにリンクします。

概念データモデルを拡張する拡張スキーマの設定について詳しくは、「スキーマエディションにつ [いて」を参照してくださ](../../configuration/using/about-schema-edition.md)い。

>[!IMPORTANT]
>
>データモデルの拡張は、上級ユーザー向けに予約されています。
