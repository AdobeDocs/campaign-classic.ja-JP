---
product: campaign
title: Adobe Campaignでのスキーマの概要
description: スキーマを使用する方法とAdobe Campaignデータベースの概念的データモデルを拡張する方法について説明します。
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Schema Extension
role: Data Engineer, Developer
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
source-git-commit: bd1007ffcfa58ee60fdafa424c7827e267845679
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 50%

---

# スキーマの基本を学ぶ {#about-schema-reference}

## スキーマとは {#what-is-a-schema}

この章では、Adobe Campaignデータベースの概念的データモデルを拡張するために拡張スキーマを設定する方法について説明します。

Campaign の組み込みテーブルとそのインタラクションについて詳しくは、 [Campaign Classicデータモデル](about-data-model.md).

Adobe Campaignでは、アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。 A **スキーマ** は、データベーステーブルに関連付けられた XML ドキュメントです。 この中でデータ構造を定義し、表の SQL 定義を記述します。

* テーブルの名前
* フィールド
* インデックス
* 他のテーブルとのリンク

また、データの格納に使用する XML 構造についても説明します。

* 要素と属性
* 要素の階層
* 要素と属性の種類
* デフォルト値
* ラベル、説明およびその他のプロパティ。

スキーマを使用すると、データベース内にエンティティを定義できます。エンティティごとにスキーマがあります。

次の図に、Adobe Campaignデータシステム内のスキーマの場所を示します。

![](assets/reference_schema_intro.png)

## スキーマの構文 {#syntax-of-schemas}

スキーマのルート要素は **`<srcschema>`** です。**`<element>`** と **`<attribute>`** のサブ要素が含まれます。

最初の **`<element>`** サブ要素は、エンティティのルートに一致します。

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">  
    <attribute name="lastName"/>
    <attribute name="email"/>
    <element name="location">
      <attribute name="city"/>
   </element>
  </element>
</srcSchema>
```

>[!NOTE]
>
>エンティティのルート要素はスキーマと同じ名前を持ちます。

![](assets/s_ncs_configuration_schema_and_entity.png)

**`<element>`** タグはエンティティ要素の名前を定義します。スキーマの **`<attribute>`** タグは、リンク先の **`<element>`** タグの属性の名前を定義します。

## スキーマの ID {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、一連のスキーマを目標領域別にグループ化できます。例えば、**cus** 名前空間は、顧客固有の設定（**customers**）に使用します。

スキーマの識別キーは、コロンで区切られた名前空間と名前を使用して作成される文字列です。次に例を示します。 **cus:recipient**.

>[!IMPORTANT]
>
>名前空間の名前は簡潔で、XML 命名規則に従って許可された文字のみを含める必要があります。
>
>識別子の先頭を数字にすることはできません。
>
>次の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明用に予約されており、使用しないでください。 **xtk**, **nl**, **nms**, **ncm**, **temp**, **ncl**, **crm**, **xxl**.

