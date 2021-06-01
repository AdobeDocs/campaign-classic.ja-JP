---
product: campaign
title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 964f1027-627c-4f12-91b5-f258e9ba458b
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 15%

---

# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

## 概要 {#overview}

アプリケーションが既存のテーブル、SQLビュー、またはリモート・データベースのデータにアクセスする必要がある場合は、次のデータを使用してAdobe Campaignでスキーマを作成します。

* テーブル名：「sqltable」属性を使用して、テーブルの名前（dblinkを使用する場合のエイリアス）を入力します。
* スキーマキー：紐付けフィールドの参照
* インデックス：クエリの生成に使用
* XML構造内のフィールドとその場所：アプリケーションで使用するフィールドにのみ入力します。
* リンク：ベースの他のテーブルとの結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージに従います。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードを編集し、「**[!UICONTROL 新規]**」をクリックします。
1. 「既存のテーブルまたはSQLビューからデータにアクセス&#x200B;]**」オプションを選択し、「**[!UICONTROL &#x200B;次へ&#x200B;]**」をクリックします。**[!UICONTROL 

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存のビューを選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. ニーズに合わせてスキーマのコンテンツを調整します。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成SQLスクリプトを生成しないように、 `<srcSchema>`ルート要素にview=&quot;true&quot;属性を設定する必要があります。

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

「**Federated Data Access - FDA**」オプションを使用すると、外部データベースに格納されたデータにアクセスできます。

外部データベースのデータにアクセスするためにスキーマに対して実行される設定については、[このページ](../../installation/using/creating-data-schema.md)で詳しく説明します。
