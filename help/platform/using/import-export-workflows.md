---
product: campaign
title: ワークフローを使用したデータのインポートとエクスポート
description: Campaign でワークフローを使用してデータをインポートおよびエクスポートする方法について学ぶ
feature: Data Management, Workflows
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
exl-id: 266ecd49-7101-4ff1-941f-1f9b39b44955
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: ht
source-wordcount: '279'
ht-degree: 100%

---

# ワークフローを使用したデータのインポートとエクスポート {#import-export-workflows}



## データの収集 {#collecting-data-workflows}

ワークフローは、一部のインポート処理を自動化する有効な手段になります。データをローカルファイルからインポートするか、SFTP からインポートするかに関係なく、ワークフローを使用してデータ管理手順を標準化することができます。

### リストからのデータの使用：リスト読み込み {#using-data-from-a-list--read-list}

ワークフローに送られるデータを、事前にデータが準備され、構造化されているリストから取り出すこともできます。

このリストは、Adobe Campaign 内に直接作成されている場合も、「**[!UICONTROL リストをインポート]**」オプションを使用してインポートされる場合もあります。このオプションについて詳しくは、この[ページ](../../platform/using/about-generic-imports-exports.md)を参照してください。

ワークフローでのリスト読み込みアクティビティの使用について詳しくは、[こちらのページ](../../workflow/using/read-list.md)を参照してください。

### ファイルからのデータの読み込み {#loading-data-from-a-file}

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

## データのエクスポート {#exporting-data-via-a-workflow}

ワークフローは、エクスポート処理の一部を自動化したり、データの変換に使用できるデータ管理アクティビティの一部を使用した後に正確なデータセットをエクスポートしたりするための有効な手段になります。

エクスポート操作は、**[!UICONTROL データ抽出（ファイル）アクティビティ]**&#x200B;を使用して実行されます。 アクティビティの設定と使用方法について詳しくは、[こちらのページ](../../workflow/using/extraction--file-.md)を参照してください。
