---
title: スキーマの特性
seo-title: スキーマの特性
description: スキーマの特性
seo-description: null
page-status-flag: never-activated
uuid: ca8eb7af-ef22-403a-8f04-ece5dc903174
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: 441e80e1-0559-41fd-83e8-afdf94279e75
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# スキーマの特性{#schema-characteristics}

既存の表を参照するスキーマの特性は次のとおりです。

* Adobe Campaignでは、既存のテーブルを基準にSQLオブジェクトを変更しないでください。
* テーブルと列の名前は、明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!CAUTION]
>
>標準受信者テーブルのフィールドは、役に立たない場合でも削除しないでください。 これは、Adobe Campaignデータベースで動作エラーが発生する可能性があります。

## ビュー属性 {#the-view-attribute}

ソーススキーマは、 **srcSchemaルート要素** のview **属性を受け入** れます。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 view=&quot; **** true&quot;属性は、このスキーマを無視するようにデータベース構造の更新ウィザードに指示します。 したがって、アプリケーションは、テーブル、そのカラム、およびそのインデックスを対応するスキーマと同期することを禁止します。

この属性を **trueに設定した場合**、スキーマは、このテーブルのデータにアクセスするSQLクエリを生成する目的でのみ使用されます。

## テーブルと列の名前 {#names-of-tables-and-columns}

テーブルの更新ウィザードでテーブルを作成すると、各スキーマと属性の名前に基づいて、テーブルと列の名前が自動的に生成されます。 ただし、次の属性を入力することで、SQL名の使用を強制できます。

* **スキーマの** メイン要素内にあるsqltable。テーブルを指定するには、
* **各属性内のsqlname** 。列を指定します。

**例**：

```
<element label="Individual" name="individual" sqltable="individual">
    <key internal="true" name="id">
      <keyfield xpath="@id"/>
    </key> 
    <attribute name="id" type="long" length="32" />
    <attribute name="lastName" type="string" length="100" sqlname="Last_Name"/>
    <attribute name="firstName" type="string" length="100" sqlname="First_Name"/>
    <attribute name="email" type="string" length="100"/>
    <attribute name="mobile" type="string" length="100"/>
</element>
```

この例では、テーブルと列の名前が明示的に指定されていない場合、アプリケーションはテーブルに **CusIndividual** 、列に **lastName** 、列に **** firstNameを使用していました。

スキーマでは、既存のテーブルの列の一部のみにデータを埋め込むことができます。 未入力の列はユーザーにアクセスできません。

## インデックス付きフィールド {#indexed-fields}

リストのレコードをクライアントコンソールから並べ替える場合、インデックス付きフィールドを並べ替えるとパフォーマンスが向上します。 スキーマでインデックスを宣言すると、コンソールに、列ラベルの左にある並べ替え順序矢印の下に、インデックス付きのフィールドが赤い線で表示されます。

![](assets/s_ncs_integration_mapping_index.png)

スキーマでは、インデックスは次のように定義されます。

```
<dbindex name="name_of_index" unique="true/false"
  <keyfield xpath="xpath_1st_field"/
  <keyfield xpath="xpath_2nd_field"/
  ...
</dbindex
```

そのため、カスタムテーブルの既存のインデックスを一致するスキーマに宣言することが重要です。

インデックスは、ソーススキーマの各キーとリンク宣言に対して暗黙的に宣言されます。 インデックス宣言は、noDbIndex=&quot;true&quot;属 **性を指定することで防ぐことができ** ます。

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```

