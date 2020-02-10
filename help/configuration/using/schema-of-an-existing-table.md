---
title: 既存のテーブルのスキーマ
seo-title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
seo-description: null
page-status-flag: never-activated
uuid: cb766259-8ed7-40a1-8df7-75a8a3f9986d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 6877d94d-d6e5-4080-a537-ef1bb6e6f8cf
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e7ff12260d875b85256c8678fa8d100fd355398e

---


# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

## 概要 {#overview}

アプリケーションが既存の表、SQLビューまたはリモートデータベースのデータにアクセスする必要がある場合は、次のデータを含むスキーマをAdobe Campaignで作成します。

* テーブル名：「sqltable」属性を使用して、テーブルの名前（DBリンクを使用する場合は別名）を入力します。
* スキーマキー：調整フィールドを参照する場合、
* インデックス：クエリーを生成するために使用され、
* XML構造内のフィールドとその場所：アプリで使用するフィールドにのみ入力し、
* リンク：ベースの他のテーブルとの結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージを適用します。

1. Adobe Campaignツリー **[!UICONTROL Administration>Configuration>Data schemas]** のノードを編集し、をクリックしま **[!UICONTROL New]** す。
1. オプションを選 **[!UICONTROL Access data from an existing table or an SQL view]** 択し、をクリックしま **[!UICONTROL Next]** す。

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存のビューを選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. ニーズに合わせてスキーマのコンテンツを調整します。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成SQLスクリプトを生成しないように、スキーマに `<srcSchema>` root要素のview=&quot;true&quot;属性を設定する必要があります。

**例**：

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

「 **Federated Data Access - FDA** 」オプションを使用すると、外部データベースに保存されているデータにアクセスできます。

外部データベースのデータにアクセスするためにスキーマに対して実行する設定については、このページで [詳しく説明しま](../../platform/using/accessing-an-external-database.md#creating-the-data-schema)す。
