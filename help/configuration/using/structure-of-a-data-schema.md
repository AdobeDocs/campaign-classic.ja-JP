---
product: campaign
title: データスキーマの構造
description: データスキーマの構造
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 86036f2f-ec7c-413e-b1e1-10a71a06cd6d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---

# データスキーマの構造{#structure-of-a-data-schema}

データスキーマの構造は、ツリー構造の形式で表示されます。 Adobe Campaignクライアントコンソールでグラフィカルに表示するには、ターゲットスキーマを選択し、「**[!UICONTROL 構造]**」サブタブをクリックします。

![](assets/d_ncs_integration_schema_arbo.png)

標準として、最初にフィールドが表示されます（アクティブ、アクティブな、など）。 とをアルファベット順に並べます。 構造化要素は次に表示されます（住所、場所）。最後に、リンク（電子メール情報、フォルダーなど）。

プライマリキーは赤色のキーで識別され、外部キーは黄色のキーで識別されます。

リンクは、テーブルに属しているかどうかに応じて視覚的に区別されます。 テーブルから始まる、つまり、テーブルに外部キーが含まれているものが最初に表示されます（電子メール情報、フォルダ、国）。 「取り消し」の収集リンク（購読、注文など） が最後に表示されます。
