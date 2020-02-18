---
title: 外部データベースへのアクセス
seo-title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: d2758b5e81d1720a4f01a610e51c4a33995d88d1

---


# ワークフローでの外部データベースからのデータの使用 {#using-data-from-an-external-database-in-a-workflow}

複数の Adobe Campaign ワークフローアクティビティで、外部データベースに格納されたデータを使用できます。

## 外部データのフィルタリング {#filtering-on-external-data}

「クエリ」アクティビティでは、外部データを追加して、定義したフィルター設定でそのデータを使用できます。

詳しくは、[クエリ](../../workflow/using/targeting-data.md#selecting-data)の節を参照してください。

## サブセットの作成 {#creating-sub-sets}

「分割」アクティビティでは、サブセットを作成できます。外部データを使用して、使用するフィルタリング条件を定義できます。

詳しくは、[分割](../../workflow/using/split.md)の節を参照してください。

## 外部データベースの読み込み {#loading-external-database}

「データの読み込み（RDBMS）」で外部データを使用できます。このアクティビティについては、[データの読み込み](../../workflow/using/data-loading--rdbms-.md)の節で説明しています。

## 情報およびリンクの追加 {#adding-information-and-links}

「エンリッチメント」アクティビティでは、ワークフローの作業用テーブルにデータを追加したり、リンクを外部テーブルに追加したりすることができます。このため、外部データベースからのデータを活用できます。この手順は、[エンリッチメント](../../workflow/using/enrichment.md)の節で説明しています。
