---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classicのスキーマリファレンスについて
description: Adobe Campaign Classicデータベースの概念データモデルを拡張するための拡張スキーマの構成方法を学びます。
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 7%

---


# スキーマリファレンスについて{#about-schema-reference}

この章では、Adobe Campaignデータベースの概念的データモデルを拡張するための拡張スキーマの設定方法について説明します。

キャンペーンの組み込みテーブルとそのやり取りについての詳細は、[Campaign Classicデータモデル](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)を参照してください。

アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。**スキーマ**&#x200B;と呼ばれるAdobe Campaign固有の文法に従います。

スキーマは、データベーステーブルに関連付けられたXMLドキュメントです。 データ構造を定義し、表のSQL定義を説明します。

* テーブルの名前
* フィールド
* インデックス
* 他のテーブルとのリンク

また、データの格納に使用するXML構造についても説明します。

* 要素と属性
* 要素の階層
* 要素と属性の種類
* デフォルト値
* ラベル、説明、およびその他のプロパティ。

スキーマを使用すると、データベース内にエンティティを定義できます。 エンティティごとにスキーマがあります。

次の図に、Adobe Campaignデータシステム内のスキーマの場所を示します。

![](assets/reference_schema_intro.png)

## スキーマの構文{#syntax-of-schemas}

スキーマのルート要素は&#x200B;**`<srcschema>`**&#x200B;です。 **`<element>`**&#x200B;と&#x200B;**`<attribute>`**&#x200B;のサブ要素が含まれます。

最初の&#x200B;**`<element>`**&#x200B;サブ要素は、エンティティのルートに一致します。

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
>エンティティのルートスキーマは、要素と同じ名前を持ちます。

![](assets/s_ncs_configuration_schema_and_entity.png)

**`<element>`**&#x200B;タグはエンティティ要素の名前を定義します。 **`<attribute>`** スキーマのタグは、リンク先の **`<element>`** タグの属性の名前を定義します。

## スキーマのID {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、スキーマのセットを目標領域別にグループ化できます。 例えば、**cus**&#x200B;名前空間は、顧客固有の設定(**customers**)に使用します。

>[!IMPORTANT]
>
>標準として、名前空間名は簡潔にし、XML命名規則に従って、許可された文字のみを含める必要があります。
>
>識別子の先頭を数字にすることはできません。

特定の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明のために予約されています。

* **xtk**:プラットフォームシステムデータについて
* **nl**:出願の全体的な使用に関して
* **nms**:配信(受信者、配信、追跡等)に関する
* **ncm**:コンテンツ管理に関して
* **temp**:一時スキーマ用に予約。

スキーマのIDキーは、名前空間と名前をコロンで区切った文字列です。例：**cus:受信者**。
