---
product: campaign
title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
feature: Custom Resources
role: Data Engineer, Developer
exl-id: 964f1027-627c-4f12-91b5-f258e9ba458b
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 9%

---

# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

## 概要 {#overview}

アプリケーションが既存のテーブル、SQL ビュー、またはリモートデータベースのデータにアクセスする必要がある場合は、次のデータを使用してAdobe Campaignでスキーマを作成します。

* テーブル名：「sqltable」属性を使用して、テーブルの名前（dblink を使用する場合は別名）を入力します。
* スキーマキー：紐付けフィールドを参照し、
* インデックス：クエリの生成に使用
* XML 構造におけるフィールドとその場所：アプリケーションで使用するフィールドのみを入力し、
* リンク：ベースの他のテーブルと結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージを適用します：

1. Adobe Campaign ツリーの **[!UICONTROL 管理/設定/データスキーマ]** ノードを編集し、「**[!UICONTROL 新規]**」をクリックします。
1. 「**[!UICONTROL 既存のテーブルまたは SQL ビューからデータにアクセス]**」オプションを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存のビューを選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. ニーズに合わせてスキーマコンテンツを調整します。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成 SQL スクリプトを生成しないようにするには、スキーマの `<srcSchema>` ルート要素に view=&quot;true&quot;属性を入力する必要があります。

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

「**Federated Data Access - FDA**」オプションを使用すると、外部データベースに保存されたデータにアクセスできます。

外部データベースのデータにアクセスするためにスキーマに実行する設定について詳しくは、[&#x200B; このページ &#x200B;](../../installation/using/creating-data-schema.md) を参照してください。
