---
solution: Campaign Classic
product: campaign
title: データスキーマの構造
description: データスキーマの構造
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---


# データスキーマの構造{#structure-of-a-data-schema}

データスキーマの構造は、ツリー構造の形式で表示されます。 これをAdobe Campaignクライアントコンソールでグラフィカルに表示するには、ターゲットスキーマを選択し、「**[!UICONTROL 構造]**」サブタブをクリックします。

![](assets/d_ncs_integration_schema_arbo.png)

標準として、最初にフィールドが表示されます（アクティブ、アクティブなど）。 とアルファベット順に並べられます。 構造化要素の次に、（住所、場所）、最後にリンク（電子メール情報、フォルダーなど）が表示されます。

プライマリキーは赤いキーで識別され、外部キーは黄色のキーで識別されます。

リンクは、テーブルに属しているかどうかに応じてグラフで区別されます。 テーブルの開始（テーブルに外部キーが含まれている）が最初に表示されます（電子メール情報、フォルダ、国）。 「逆」の収集リンク(購読、注文件数など) 」が最後に表示されます。
