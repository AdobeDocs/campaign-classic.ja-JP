---
solution: Campaign Classic
product: campaign
title: ワークフローを使用したデータのインポートとエクスポート
description: Campaign Classic でワークフローを使用してデータをインポートおよびエクスポートする方法について説明します。
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
translation-type: tm+mt
source-git-commit: b05b8daad449aeb1f5226fdd76744776c6553b63
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 92%

---


# ワークフロー{#import-export-workflows}を使用したデータのインポートとエクスポート

## データの収集 {#collecting-data-workflows}

ワークフローは、一部のインポート処理を自動化する有効な手段になります。データをローカルファイルからインポートするか、SFTP からインポートするかに関係なく、ワークフローを使用してデータ管理手順を標準化することができます。

### リストのデータを使用する：リスト読み込み{#using-data-from-a-list--read-list}

ワークフローに送られるデータを、事前にデータが準備され、構造化されているリストから取り出すこともできます。

このリストは、Adobe Campaign 内に直接作成されている場合も、「**[!UICONTROL リストをインポート]**」オプションを使用してインポートされる場合もあります。このオプションについて詳しくは、この[ページ](../../platform/using/about-generic-imports-exports.md)を参照してください。

ワークフローでのリスト読み込みアクティビティの使用について詳しくは、[こちらのページ](../../workflow/using/read-list.md)を参照してください。

### ファイル{#loading-data-from-a-file}からデータをロード

ワークフロー内で処理されるデータは、Adobe Campaign にインポートできるように、構造化ファイルから抽出することができます。

データアクティビティの読み込みについて詳しくは、[データ読み込み（ファイル）](../../workflow/using/data-loading--file-.md)の節を参照してください。

インポートする構造化ファイルの例：

```
lastname;firstname;birthdate;email;crmID
Smith;Hayden;23/05/1989;hayden.smith@example.com;124365
Mars;Daniel;17/11/1987;dannymars@example.com;123545
Smith;Clara;08/02/1989;hayden.smith@example.com;124567
Durance;Allison;15/12/1978;allison.durance@example.com;120987
```

データを収集したら、ワークフローで配信の拡充やデータベースの更新などに使用できます。詳しくは、[こちらのページ](../../workflow/using/how-to-use-workflow-data.md)を参照してください。

## データのエクスポート{#exporting-data-via-a-workflow}

ワークフローは、エクスポート処理の一部を自動化したり、データの変換に使用できるデータ管理アクティビティの一部を使用した後に正確なデータセットをエクスポートしたりするための有効な手段になります。

エクスポート操作は、**[!UICONTROL データ抽出（ファイル）アクティビティ]**&#x200B;を使用して実行されます。 アクティビティの設定と使用方法について詳しくは、[こちらのページ](../../workflow/using/extraction--file-.md)を参照してください。
