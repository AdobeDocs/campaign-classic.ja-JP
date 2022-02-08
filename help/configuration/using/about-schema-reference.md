---
product: campaign
title: Adobe Campaign Classicのスキーマリファレンスについて
description: Adobe Campaign Classicデータベースの概念的データモデルを拡張するための拡張スキーマの設定方法について説明します。
feature: Schema Extension
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
source-git-commit: 8fa50d17a9ff36ccc310860ac93771590cfd76fd
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 58%

---

# スキーマリファレンスについて{#about-schema-reference}

![](../../assets/v7-only.svg)

この章では、Adobe Campaignデータベースの概念的データモデルを拡張するために拡張スキーマを設定する方法について説明します。

Campaign の組み込みテーブルとそのインタラクションについて詳しくは、 [Campaign Classicデータモデル](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html).

アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。 **スキーマ**&#x200B;と呼ばれる Adobe Campaign 特有の文法に従います。

スキーマは、データベーステーブルに関連付けられた XML ドキュメントです。 この中でデータ構造を定義し、表の SQL 定義を記述します。

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

スキーマを使用すると、データベース内にエンティティを定義できます。 エンティティごとにスキーマがあります。

次の図に、Adobe Campaignデータシステム内のスキーマの場所を示します。

![](assets/reference_schema_intro.png)

## スキーマの構文 {#syntax-of-schemas}

スキーマのルート要素は **`<srcschema>`** です。 **`<element>`** と **`<attribute>`** のサブ要素が含まれます。

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

**`<element>`** タグはエンティティ要素の名前を定義します。 スキーマの **`<attribute>`** タグは、リンク先の **`<element>`** タグの属性の名前を定義します。

## スキーマの ID {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、一連のスキーマを目標領域別にグループ化できます。 例えば、**cus** 名前空間は、顧客固有の設定（**customers**）に使用します。

スキーマの識別キーは、コロンで区切られた名前空間と名前を使用して作成された文字列です。例： **cus:recipient**.

>[!IMPORTANT]
>
>名前空間の名前は簡潔で、XML 命名規則に従って許可された文字のみを含める必要があります。
>
>識別子の先頭を数字にすることはできません。
>
>次の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明用に予約されており、使用しないでください。 **xtk**, **nl**, **nms**, **ncm**, **temp**, **ncl**, **crm**, **xxl**.

