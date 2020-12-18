---
solution: Campaign Classic
product: campaign
title: 既存のテーブルのスキーマ
description: 既存のテーブルのスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 9%

---


# 既存のテーブルのスキーマ{#schema-of-an-existing-table}

## 概要 {#overview}

既存の表、SQL表示、またはリモート・データベースからのデータにアクセスする必要がある場合は、次のデータを使用してAdobe Campaignでスキーマを作成します。

* テーブル名：「sqltable」属性を使用して、テーブルの名前（dblinkを使用する場合は別名）を入力します。
* スキーマキー：調整フィールドを参照する
* インデックス：クエリの生成に使用され、
* XML構造内のフィールドとフィールドの場所：申込書で使用されているフィールドにのみ入力します。
* リンク：ベースの他のテーブルとの結合がある場合。

## 実装 {#implementation}

対応するスキーマを作成するには、次のステージを適用します。

1. Adobe Campaignツリーの&#x200B;**[!UICONTROL Administration>Configuration>Dataスキーマー]**&#x200B;ノードを編集し、**[!UICONTROL New]**&#x200B;をクリックします。
1. 「**[!UICONTROL 既存のテーブルまたはSQL表示からデータにアクセス]**」オプションを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_configuration_extand_a_schema.png)

1. テーブルまたは既存の表示を選択します。

   ![](assets/s_ncs_configuration_select_table.png)

1. 必要に応じてスキーマの内容を調整します。

   ![](assets/s_ncs_configuration_view_create_schema.png)

   テーブル作成SQLスクリプトを生成しないように、スキーマに`<srcSchema>`ルート要素の表示=&quot;true&quot;属性を設定する必要があります。

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

**Federated Data Access-FDA**&#x200B;オプションを使用すると、外部データベースに格納されたデータにアクセスできます。

外部データベース内のデータにアクセスするスキーマに対して行う構成は、[このページ](../../installation/using/creating-data-schema.md)に詳しく記載されています。
