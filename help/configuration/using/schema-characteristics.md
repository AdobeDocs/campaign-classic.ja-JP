---
product: campaign
title: スキーマの特性
description: スキーマの特性
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 099161b4-b4cb-433c-aed6-71157269a536
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 2%

---

# スキーマの特性{#schema-characteristics}

既存のテーブルを参照するスキーマの特性は次のとおりです。

* Adobe Campaignは、既存のテーブルに対するSQLオブジェクトを変更できません。
* テーブルと列の名前は、明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>標準の受信者テーブルのフィールドは、役に立たないものでも削除しないでください。 これにより、Adobe Campaignデータベースで動作エラーが発生する可能性があります。

## ビュー属性{#the-view-attribute}

ソーススキーマは、**srcSchema**&#x200B;ルート要素の&#x200B;**view**&#x200B;属性を受け取ります。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 **view=&quot;true&quot;**&#x200B;属性は、データベース構造の更新ウィザードに対し、このスキーマを無視するよう指示します。 したがって、アプリケーションは、テーブル、その列およびそのインデックスを対応するスキーマと同期することを禁止します。

この属性を&#x200B;**true**&#x200B;に設定した場合、スキーマは、このテーブルのデータにアクセスするSQLクエリを生成する目的でのみ使用されます。

## テーブルと列の名前{#names-of-tables-and-columns}

テーブルの更新ウィザードでテーブルを作成すると、各スキーマと属性の名前に基づいて、テーブルと列の名前が自動的に生成されます。 ただし、次の属性を入力することで、SQL名の使用を強制できます。

* **** sqltable（スキーマのメイン要素内）に、テーブルを指定します。
* **** sqlnameを各属性内に追加して、列を指定します。

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

この例で、テーブルと列の名前が明示的に指定されていない場合、アプリケーションは、テーブルに&#x200B;**CusIndividual**&#x200B;を使用し、テーブルに&#x200B;**lastName**&#x200B;および&#x200B;**firstName**&#x200B;を使用します。

スキーマでは、既存のテーブルの列の一部のみを入力できます。 未入力の列は、ユーザーがアクセスできなくなります。

## インデックス付きのフィールド{#indexed-fields}

クライアントコンソールからリストのレコードを並べ替える場合、インデックス付きのフィールドを並べ替えると、パフォーマンスが向上します。 スキーマでインデックスを宣言すると、次に示すように、コンソールに、列ラベルの左側にある並べ替え順矢印の下に赤い線の付いたインデックス付きフィールドが表示されます。

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

ソーススキーマの各キーおよびリンク宣言に対して、インデックスが暗黙的に宣言されます。 インデックス宣言は、**noDbIndex=&quot;true&quot;**&#x200B;属性を指定することで回避できます。

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```
