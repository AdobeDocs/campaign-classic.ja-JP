---
solution: Campaign Classic
product: campaign
title: スキーマの特性
description: スキーマの特性
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 2%

---


# スキーマの特性{#schema-characteristics}

既存のテーブルを参照するスキーマの特性は次のとおりです。

* Adobe Campaignは、既存のテーブル、
* テーブルと列の名前は、明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>使用できない場合でも、標準受信者テーブルのフィールドを削除しないでください。 これは、Adobe Campaignデータベースで動作エラーを引き起こす可能性があります。

## 表示属性{#the-view-attribute}

ソーススキーマは、**srcSchema**&#x200B;ルート要素の&#x200B;**表示**&#x200B;属性を受け入れます。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 **表示=&quot;true&quot;**&#x200B;属性は、データベース構造の更新ウィザードに対して、このスキーマを無視するよう指示します。 したがって、テーブル、その列、およびそのインデックスを対応するスキーマと同期するのは禁止されます。

この属性が&#x200B;**true**&#x200B;に設定されている場合、スキーマは、このテーブルのデータにアクセスするSQLクエリを生成する目的でのみ使用されます。

## テーブルと列の名前{#names-of-tables-and-columns}

テーブルの更新ウィザードでテーブルを作成すると、各スキーマと属性の名前に基づいて、テーブルと列の名前が自動的に生成されます。 ただし、次の属性を入力して、SQL名の使用を強制できます。

* **スキーマのメイン要素内の** sqltableを指定し、テーブル、
* **各属性内の** sqlname。列を指定します。

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

この例で、テーブルと列の名前が明示的に指定されていない場合、アプリケーションはテーブルに&#x200B;**CusIndividual**&#x200B;を、列に&#x200B;**lastName**&#x200B;と&#x200B;**firstName**&#x200B;を使用していました。

スキーマでは、既存のテーブルの列の一部のみを埋め込むことができます。 入力されていない列は、ユーザーはアクセスできません。

## インデックス付きフィールド{#indexed-fields}

リストのレコードをクライアントコンソールから並べ替える場合、インデックス付きのフィールドを並べ替えるとパフォーマンスが向上します。 スキーマでインデックスを宣言すると、以下に示すように、コンソールに、列ラベルの左にある並べ替え順矢印の下に、インデックス付きのフィールドが赤い線で表示されます。

![](assets/s_ncs_integration_mapping_index.png)

スキーマでは、インデックスは次のように定義されます。

```
<dbindex name="name_of_index" unique="true/false"
  <keyfield xpath="xpath_1st_field"/
  <keyfield xpath="xpath_2nd_field"/
  ...
</dbindex
```

そのため、カスタムテーブルの既存のインデックスを一致するスキーマで宣言することが重要です。

ソーススキーマの各キーとリンク宣言に対してインデックスが暗黙的に宣言されます。 **noDbIndex=&quot;true&quot;**&#x200B;属性を指定すると、インデックスの宣言を防ぐことができます。

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```

