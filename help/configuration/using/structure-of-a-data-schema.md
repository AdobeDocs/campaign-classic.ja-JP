---
title: データスキーマの構造
seo-title: データスキーマの構造
description: データスキーマの構造
seo-description: null
page-status-flag: never-activated
uuid: 83e3995d-fa31-4cb5-acf2-83f17329c99c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: a1a39eaa-6d6f-42c5-a36b-bd1cb3a77dcb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# Structure of a data schema{#structure-of-a-data-schema}

データスキーマの構造は、ツリー構造の形で表示されます。 Adobe Campaignクライアントコンソールでグラフィカルに表示するには、対象となるスキーマを選択し、サブタブを **[!UICONTROL Structure]** クリックします。

![](assets/d_ncs_integration_schema_arbo.png)

標準として、最初にフィールドが表示されます（アクティブ、アクティブなど）。とアルファベット順に並べられます。 構造化要素の次に、（住所、場所）、最後にリンク（電子メール情報、フォルダーなど）が表示されます。

主キーは赤のキーで識別され、外部キーは黄色のキーで識別されます。

リンクは、テーブルに属しているかどうかに応じてグラフで区別されます。 テーブルから開始する、つまりテーブルに外部キーが含まれている場合は、最初に表示されます（電子メール情報、フォルダ、国）。 「逆」の収集リンク（購読、注文件数など）が最後に表示されます。
