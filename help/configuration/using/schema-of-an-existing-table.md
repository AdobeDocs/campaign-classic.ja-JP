---
product: campaign
title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
feature: Custom Resources
role: Developer
exl-id: 964f1027-627c-4f12-91b5-f258e9ba458b
TQID: https://experienceleague.adobe.com/Vi1DhgY8tGIhq1TtMOGKeGMrqFgGecfJQHrKyFXTSgg
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 232
ht-degree: 9%

---

# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

## 概要 {#overview}

アプリケーションが既存のテーブル、SQL ビュー、またはリモートデータベースからのデータにアクセスする必要がある場合は、次のデータを使用してAdobe Campaignでスキーマを作成します。

* テーブルの名前：&quot;sqltable&quot;属性を持つテーブルの名前（dblinkを使用する場合はエイリアスを含む）を入力します。
* スキーマキー：紐付けフィールドを参照し、
* インデックス：クエリの生成に使用されます。
* XML構造内のフィールドとその場所：アプリケーションで使用されるフィールドのみを入力し、
* リンク：ベースの他のテーブルとの結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージを適用します。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理>設定> データスキーマ]** ノードを編集し、**[!UICONTROL 新規]**&#x200B;をクリックします。
1. 既存のテーブルまたはSQL ビュー&#x200B;**オプションから** データにアクセスを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存のビューを選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. ニーズに合わせてスキーマコンテンツを適応させます。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成SQL スクリプトを生成しないように、スキーマに`<srcSchema>` ルート要素のview=&quot;true&quot;属性を入力する必要があります。

**例** :

```
<srcSchema name="recipient" namespace="cus" view="true">
  <element name="recipient" sqltable="dbsrv.recipient">
    <key name="email">
      <keyfield xpath="@email"/>
    </key>   
    <attribute name="email" type="string" length="80" sqlname="email"/>
  </element>
</srcSchema>
```

## 外部データベースへのアクセス {#accessing-an-external-database}

**Federated Data Access - FDA** オプションを使用すると、外部データベースに保存されているデータにアクセスできます。

外部データベースのデータにアクセスするためにスキーマで実行する設定については、[このページ &#x200B;](../../installation/using/creating-data-schema.md)で詳しく説明しています。
