---
product: campaign
title: Adobe Campaign Classicのスキーマリファレンスについて
description: Adobe Campaign Classicデータベースの概念的データモデルを拡張するための拡張スキーマの設定方法について説明します。
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 61%

---

# スキーマリファレンスについて{#about-schema-reference}

この章では、Adobe Campaignデータベースの概念的データモデルを拡張するための拡張スキーマの設定方法について説明します。

Campaignの組み込みテーブルとそのインタラクションについての詳細は、[Campaign Classicデータモデル](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)を参照してください。

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

>[!IMPORTANT]
>
>基準としては、名前空間の名前は簡潔なものにし、XML 命名規則に従って許可された文字のみで構成する必要があります。
>
>識別子の先頭を数字にすることはできません。

特定の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明用に予約されています。

* **xtk**:プラットフォームシステムデータに関して
* **nl**:アプリケーションの全体的な使用に関して
* **nms**:配信（受信者、配信、トラッキングなど）に関して
* **ncm**:コンテンツ管理に関して
* **temp**:一時的なスキーマ用に予約されています。

スキーマの識別キーは、コロンで区切られた名前空間と名前を使用して構築された文字列です。例：**cus:recipient**&#x200B;とします。
