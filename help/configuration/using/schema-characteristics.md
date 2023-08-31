---
product: campaign
title: スキーマの特性
description: スキーマの特性
feature: Custom Resources
role: Data Engineer, Developer
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 099161b4-b4cb-433c-aed6-71157269a536
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 5%

---

# スキーマの特性{#schema-characteristics}



既存のテーブルを参照するスキーマの特性は次のとおりです。

* Adobe Campaignは、既存のテーブルに対する SQL オブジェクトを変更できません。
* テーブルと列の名前は、明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>組み込みの受信者テーブルのフィールドは、役に立たないフィールドでも削除しないでください。 これにより、Adobe Campaignデータベースで動作エラーが発生する可能性があります。

## ビュー属性 {#the-view-attribute}

ソーススキーマは、 **表示** の属性 **srcSchema** ルート要素を使用します。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 The **view=&quot;true&quot;** 属性は、データベース構造の更新ウィザードに対して、このスキーマを無視するよう指示します。 したがって、アプリケーションは、テーブル、その列およびそのインデックスを対応するスキーマと同期することはできません。

この属性が **true**&#x200B;の場合、スキーマは、このテーブルのデータにアクセスする SQL クエリを生成する目的でのみ使用されます。

## テーブルおよび列の名前 {#names-of-tables-and-columns}

テーブルの更新ウィザードでテーブルを作成すると、テーブルと列の名前が、それぞれのスキーマと属性の名前に基づいて自動的に生成されます。 ただし、次の属性を入力することで、SQL 名の使用を強制できます。

* **sqltable** スキーマのメイン要素内で、テーブルを指定します。
* **sqlname** 各属性内で、列を指定します。

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

この例では、テーブルと列の名前が明示的に指定されていない場合、アプリケーションは **CusIndividual** テーブルの **lastName** および **firstName** 列に対して。

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

そのため、一致するスキーマ内でカスタムテーブルの既存のインデックスを宣言することが重要です。

インデックスは、ソーススキーマの各キーおよびリンク宣言に対して暗黙的に宣言されます。 インデックスの宣言は、 **noDbIndex=&quot;true&quot;** 属性：

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```
