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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 13%

---


# データスキーマの構造{#structure-of-a-data-schema}

データスキーマの構造は、ツリー構造の形式で表示されます。 Adobe Campaignクライアントコンソールでグラフィカルに表示するには、ターゲットスキーマを選択し、「 **[!UICONTROL 構造]** 」サブタブをクリックします。

![](assets/d_ncs_integration_schema_arbo.png)

標準として、最初にフィールドが表示されます（アクティブ、アクティブなど）。 とアルファベット順に並べられます。 構造化要素の次に、（住所、場所）、最後にリンク（電子メール情報、フォルダーなど）が表示されます。

プライマリキーは赤いキーで識別され、外部キーは黄色のキーで識別されます。

リンクは、テーブルに属しているかどうかに応じてグラフで区別されます。 テーブルの開始（テーブルに外部キーが含まれている）が最初に表示されます（電子メール情報、フォルダ、国）。 「逆」の収集リンク(購読、注文件数など) 」が最後に表示されます。
