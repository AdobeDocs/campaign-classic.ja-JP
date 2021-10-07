---
product: campaign
title: スキーマの特性
description: スキーマの特性
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 099161b4-b4cb-433c-aed6-71157269a536
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 2%

---

# スキーマの特性{#schema-characteristics}

![](../../assets/v7-only.svg)

既存のテーブルを参照するスキーマの特性を次に示します。

* Adobe Campaignは、既存の表に対する SQL オブジェクトを変更できません。
* テーブルと列の名前は、明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>役に立たないフィールドでも、標準の受信者テーブルのフィールドを削除しないでください。 これにより、Adobe Campaignデータベースで動作エラーが発生する可能性があります。

## view 属性 {#the-view-attribute}

ソーススキーマは、**srcSchema** ルート要素の **view** 属性を受け取ります。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 **view=&quot;true&quot;** 属性は、データベース構造の更新ウィザードに対し、このスキーマを無視するよう指示します。 したがって、アプリケーションは、テーブル、その列およびそのインデックスを対応するスキーマと同期することはできません。

この属性が **true** に設定されている場合、スキーマは、このテーブルのデータにアクセスする SQL クエリを生成する目的でのみ使用されます。

## テーブルおよび列の名前 {#names-of-tables-and-columns}

表の更新ウィザードで表を作成すると、表と列の名前は、それぞれのスキーマと属性の名前に基づいて自動的に生成されます。 ただし、次の属性を入力することで、SQL 名の使用を強制できます。

* **** sqltable スキーマのメイン要素内で、テーブルを指定します。
* **** 各属性内の sqlname。列を指定します。

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

この例では、テーブルと列の名前が明示的に指定されていない場合、アプリケーションは、テーブルに **CusIndividual** を使用し、テーブルに **lastName** および **firstName** を使用しています。

スキーマでは、既存のテーブルの列の一部のみを入力できます。 未入力の列は、ユーザーがアクセスできなくなります。

## インデックス付きのフィールド {#indexed-fields}

クライアントコンソールからリストのレコードを並べ替える場合、インデックス付きのフィールドを並べ替えると、パフォーマンスが向上します。 スキーマでインデックスを宣言すると、次に示すように、コンソールに、列ラベルの左側にある並べ替え順矢印の下に赤い線が付いたインデックス付きフィールドが表示されます。

![](assets/s_ncs_integration_mapping_index.png)

スキーマでは、インデックスは次のように定義されます。

```
<dbindex name="name_of_index" unique="true/false"
  <keyfield xpath="xpath_1st_field"/
  <keyfield xpath="xpath_2nd_field"/
  ...
</dbindex
```

そのため、カスタムテーブルの既存のインデックスを、対応するスキーマで宣言することが重要です。

インデックスは、ソーススキーマの各キーおよびリンク宣言に対して暗黙的に宣言されます。 **noDbIndex=&quot;true&quot;** 属性を指定すると、インデックスの宣言を防ぐことができます。

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```
