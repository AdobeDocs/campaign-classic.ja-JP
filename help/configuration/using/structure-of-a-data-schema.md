---
product: campaign
title: データスキーマの構造
description: データスキーマの構造
feature: Custom Resources
role: Data Engineer, Developer
exl-id: 86036f2f-ec7c-413e-b1e1-10a71a06cd6d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---

# データスキーマの構造{#structure-of-a-data-schema}

データスキーマの構造は、ツリー構造で表示されます。 Adobe Campaign クライアントコンソールでグラフィカルに表示するには、ターゲットのスキーマを選択し、「**[!UICONTROL 構造]**」サブタブをクリックします。

![](assets/d_ncs_integration_schema_arbo.png)

標準では、フィールドが最初に表示されます（アクティブ、アクティブなど）。 アルファベット順におよびを並べます。 次に、構造要素（住所、場所）が来て、最後にリンク（メール情報、フォルダーなど）が来ます。

プライマリキーは赤いキー、外部キーは黄のキーで識別されます。

リンクは、テーブルに属しているかどうかに応じて、視覚的に区別されます。 テーブルから開始するキー（例：テーブルに外部キーがあるキー）は、最初に表示されます（メール情報、フォルダー、国）。 「リバース」コレクションリンク（購読、注文など） が最後に表示されます。
