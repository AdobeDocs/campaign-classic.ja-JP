---
product: campaign
title: スキーマの特性
description: スキーマの特性
feature: Custom Resources
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 099161b4-b4cb-433c-aed6-71157269a536
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# スキーマの特性{#schema-characteristics}



既存のテーブルを参照するスキーマの特性は次のとおりです。

* Adobe Campaignでは、既存のテーブルを基準とした SQL オブジェクトを変更しないでください。
* テーブルと列の名前を明示的に指定する必要があります。
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>組み込みの受信者テーブル内のフィールドは、役に立たない場合でも削除しないでください。 これにより、Adobe Campaign データベースで行動エラーが発生する可能性があります。

## ビュー属性 {#the-view-attribute}

ソーススキーマは、を受け入れます **表示** の属性 **srcSchema** ルート要素。 カスタムテーブルでAdobe Campaignを操作する場合に使用する必要があります。 この **view=&quot;true&quot;** 属性は、このスキーマを無視するようにデータベース構造更新ウィザードに指示します。 したがって、アプリケーションは、テーブル、その列およびインデックスを対応するスキーマと同期させることを禁止されています。

この属性を次のように設定すると、 **true**：スキーマは、このテーブルのデータにアクセスする SQL クエリを生成するためにのみ使用されます。

## テーブルと列の名前 {#names-of-tables-and-columns}

テーブル更新ウィザードでテーブルを作成すると、それぞれのスキーマと属性の名前に基づいて、テーブルと列の名前が自動的に生成されます。 ただし、次の属性を入力することで、SQL 名を強制的に使用することができます。

* **sqltable** スキーマのメイン要素内で、テーブルを指定するには、
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

この例では、テーブルと列の名前が明示的に指定されていない場合、アプリケーションはを使用しています **CusIndividual** テーブルの場合、 **lastName** および **firstName** 列の場合。

スキーマでは、既存のテーブルの列の一部のみを入力することができます。 未入力の列はユーザーがアクセスできません。

## インデックス付きフィールド {#indexed-fields}

クライアントコンソールからリストのレコードを並べ替えると、インデックス付きフィールドで並べ替えることで、パフォーマンスが向上します。 スキーマでインデックスを宣言すると、次に示すように、列ラベルの左側にある並べ替え順の矢印の下に赤い線が付いたインデックス付きフィールドがコンソールに表示されます。

![](assets/s_ncs_integration_mapping_index.png)

スキーマでは、インデックスは次のように定義されます。

```
<dbindex name="name_of_index" unique="true/false"
  <keyfield xpath="xpath_1st_field"/
  <keyfield xpath="xpath_2nd_field"/
  ...
</dbindex
```

そのため、一致するスキーマ内のカスタムテーブルの既存のインデックスを宣言することが重要です。

インデックスは、ソーススキーマの各キーおよびリンク宣言に対して暗黙的に宣言されます。 インデックスの宣言は、 **noDbIndex=&quot;true&quot;** 属性：

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```
