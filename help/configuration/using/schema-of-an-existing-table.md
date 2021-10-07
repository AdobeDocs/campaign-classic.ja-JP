---
product: campaign
title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 964f1027-627c-4f12-91b5-f258e9ba458b
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 15%

---

# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

![](../../assets/v7-only.svg)

## 概要 {#overview}

アプリケーションが既存のテーブル、SQL ビュー、またはリモート・データベースのデータにアクセスする必要がある場合は、次のデータを使用してAdobe Campaignでスキーマを作成します。

* テーブル名：「sqltable」属性を使用して、テーブルの名前（dblink を使用する場合のエイリアス）を入力します。
* スキーマキー：紐付けフィールドの参照
* インデックス：クエリの生成に使用
* XML 構造内のフィールドとその場所：アプリケーションで使用するフィールドにのみ入力します。
* リンク：ベースの他のテーブルとの結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージを適用します。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードを編集し、「**[!UICONTROL 新規]**」をクリックします。
1. 「**[!UICONTROL 既存のテーブルまたは SQL ビューからデータにアクセス]**」オプションを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存のビューを選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. ニーズに合わせてスキーマのコンテンツを調整します。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成 SQL スクリプトを生成しないように、 `<srcSchema>` ルート要素の view=&quot;true&quot;属性をスキーマに設定する必要があります。

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

「**Federated Data Access - FDA**」オプションを使用すると、外部データベースに保存されているデータにアクセスできます。

外部データベースのデータにアクセスするためにスキーマに対して実行する設定について詳しくは、[ このページ ](../../installation/using/creating-data-schema.md) を参照してください。
