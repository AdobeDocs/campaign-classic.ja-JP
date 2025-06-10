---
product: campaign
title: ワークフローを使用したデータのインポートとエクスポート
description: Campaign でワークフローを使用してデータをインポートおよびエクスポートする方法について学ぶ
feature: Data Management, Workflows
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
exl-id: 266ecd49-7101-4ff1-941f-1f9b39b44955
source-git-commit: 4fb262c616276f785f97b42bec22c150afc6e5c8
workflow-type: ht
source-wordcount: '87'
ht-degree: 100%

---

# ワークフローを使用したデータのインポートとエクスポート {#import-export-workflows}



## データの収集 {#collecting-data-workflows}

ワークフローは、一部のインポート処理を自動化する有効な手段になります。データをローカルファイルからインポートするか、SFTP からインポートするかに関係なく、ワークフローを使用してデータ管理手順を標準化することができます。

>[!NOTE]
>
>ワークフローを使用したデータのインポートとエクスポートについて詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/audience/add-profiles/import-profiles){target=_blank}を参照してください。


<!--
### Use data from a list: Read list {#using-data-from-a-list--read-list}

The data sent in a workflow can come from lists whereby the data has been prepared and structured beforehand.

This list may have been directly created in Adobe Campaign or imported by the **[!UICONTROL Import a list]** option. For more on this option, refer to this [page](../../platform/using/about-generic-imports-exports.md).

For more on using the read list activity in a workflow, refer to [this page](../../workflow/using/read-list.md).

### Load data from a file {#loading-data-from-a-file}

The data processed in a workflow can be extracted from a structured file so that it can be imported into Adobe Campaign.

A description of the loading data activity can be found in the [Data loading (file)](../../workflow/using/data-loading-file.md) section.

Example of structured file to import:

```
lastname;firstname;birthdate;email;crmID
Smith;Hayden;23/05/1989;hayden.smith@example.com;124365
Mars;Daniel;17/11/1987;dannymars@example.com;123545
Smith;Clara;08/02/1989;hayden.smith@example.com;124567
Durance;Allison;15/12/1978;allison.durance@example.com;120987
```

Once data has been collected you can use it in your workflows, for example to enrich a delivery or update the database. For more on this, refer to [this page](../../workflow/using/how-to-use-workflow-data.md).

## Export data {#exporting-data-via-a-workflow}

Workflows can be a useful way to automate some of your export processes or to export precise sets of data after using some of the available data management activities available to transform your data.

Export operations are performed using a **[!UICONTROL Data extraction (file) activity]**. For more on how to configure and use the activity, refer to [this page](../../workflow/using/extraction-file.md).
-->