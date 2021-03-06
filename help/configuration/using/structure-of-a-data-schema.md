---
product: campaign
title: データスキーマの構造
description: データスキーマの構造
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 86036f2f-ec7c-413e-b1e1-10a71a06cd6d
source-git-commit: f000cb8bae164c22d1ede15db4e763cf50530674
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---

# データスキーマの構造{#structure-of-a-data-schema}

![](../../assets/v7-only.svg)

データスキーマの構造は、ツリー構造の形式で表示されます。 Adobe Campaignクライアントコンソールでグラフィカルに表示するには、ターゲットスキーマを選択し、 **[!UICONTROL 構造]** サブタブを使用します。

![](assets/d_ncs_integration_schema_arbo.png)

標準として、フィールドが最初に表示されます（アクティブ、アクティブなど）。 およびをアルファベット順に並べ替えます。 構造化要素は次に表示されます（郵送先住所、場所）。最後に、リンク（E メール情報、フォルダーなど）。

プライマリキーは赤いキーで識別され、外部キーは黄色のキーで識別されます。

リンクは、そのリンクがテーブルに属しているかどうかに応じて視覚的に区別されます。 テーブルから始まる（テーブルに外部キーが含まれる）ものが最初に表示されます（メール情報、フォルダ、国）。 「逆引き」の収集リンク（購読、注文など） が最後に表示されます。
