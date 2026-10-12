---
product: campaign
title: データベースマッピング
description: データベースマッピング
feature: Configuration, Instance Settings
role: Developer
exl-id: 728b509f-2755-48df-8b12-449b7044e317
TQID: 'https://experienceleague.adobe.com/d3oQ8zJVsjVdj9PZ30rQ8hEuern1l3ZlMAWrbymhnvs'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: 7f0a1ee5-eeb8-5478-a9cd-b1896f033118
    internal-label: Instance Settings
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a97306b73a2b577841e6f24536c62b2526e9fda9
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 19%
---
# データベースマッピング{#database-mapping}

このページでは、スキーマのフィールドでインデックスを宣言する方法について説明します。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 スキーマのSQL マッピングについて詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-mapping){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-mapping){target=_blank}

## 索引付きフィールド {#indexed-fields}

インデックスを使用すると、アプリケーションで使用されるSQL クエリのパフォーマンスを最適化できます。

インデックスは、データスキーマのメイン要素から宣言されます。

```sql
<dbindex name="name_of_index" unique="true/false">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

インデックスは次のルールに従います。

* インデックスは、テーブル内の1つ以上のフィールドを参照できます
* **unique**&#x200B;属性に「true」の値が含まれている場合、すべてのフィールドでインデックスを一意にできます（重複を避けるために）
* インデックスのSQL名は、テーブルのSQL名とインデックスの名前から決まります

>[!NOTE]
>
>* 標準として、インデックスは、スキーマのメイン要素から宣言された最初の要素です。
>
>* インデックスは、テーブルマッピング（標準またはFDA）中に自動的に作成されます。

**例**：

* メールアドレスと市区町村にインデックスを追加する：

  ```sql
  <srcSchema name="recipient" namespace="cus">
    <element name="recipient">
      <dbindex name="email">
        <keyfield xpath="@email"/> 
        <keyfield xpath="location/@city"/> 
      </dbindex>
  
      <attribute name="email" type="string" length="80" label="Email" desc="Email address of recipient"/>
      <element name="location" label="Location">
        <attribute name="city" type="string" length="50" label="City" userEnum="city"/>
      </element>
    </element>
  </srcSchema>
  ```

* 「id」名フィールドに一意のインデックスを追加する：

  ```sql
  <srcSchema name="recipient" namespace="cus">
    <element name="recipient">
      <dbindex name="id" unique="true">
        <keyfield xpath="@id"/> 
      </dbindex>
  
      <dbindex name="email">
        <keyfield xpath="@email"/> 
      </dbindex>
  
      <attribute name="id" type="long" label="Identifier"/>
      <attribute name="email" type="string" length="80" label="Email" desc="Email address of recipient"/>
    </element>
  </srcSchema>
  ```

## 詳細情報

詳細については、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [スキーマの構造](schema-structure.md)
* [鍵の管理](database-keys.md)
* [ リンク管理](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-links){target="_blank"} （Campaign v8 ドキュメント）
