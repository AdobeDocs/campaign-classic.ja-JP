---
product: campaign
title: スキーマの特性
description: スキーマの特性
feature: Custom Resources
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 099161b4-b4cb-433c-aed6-71157269a536
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 4%

---

# スキーマの特性{#schema-characteristics}



既存のテーブルを参照するスキーマの特性は次のとおりです。

* Adobe Campaignは、既存のテーブルに対してSQL オブジェクトを変更することはできません。
* テーブルと列の名前は明示的に指定する必要があります，
* インデックスを宣言する必要があります。

>[!IMPORTANT]
>
>組み込み受信者テーブルのフィールドが役に立たない場合でも、削除しないでください。 これは、Adobe Campaign データベースの動作エラーを引き起こす可能性があります。

## ビュー属性 {#the-view-attribute}

Source スキーマは、**srcSchema** ルート要素の&#x200B;**view**&#x200B;属性を受け入れます。 Adobe Campaignをカスタムテーブルで操作する場合は、このオプションを使用する必要があります。 **view=&quot;true&quot;**&#x200B;属性は、このスキーマを無視するようにデータベース構造更新アシスタントに指示します。 したがって、アプリケーションは、テーブル、その列およびインデックスを対応するスキーマと同期することを禁止されています。

この属性が&#x200B;**true**&#x200B;に設定されている場合、スキーマはこのテーブルのデータにアクセスするためのSQL クエリの生成にのみ使用されます。

## 表と列の名前 {#names-of-tables-and-columns}

テーブル更新アシスタントによってテーブルが作成されると、各スキーマと属性の名前に基づいて、テーブルと列の名前が自動的に生成されます。 ただし、次の属性を入力して、SQL名を強制的に使用することは可能です。

* スキーマのメイン要素内の&#x200B;**sqltable**。テーブルを指定するには、
* 各属性内の&#x200B;**sqlname**&#x200B;を使用して、列を指定します。

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

この例では、テーブルと列の名前が明示的に指定されていない場合、アプリケーションはテーブルに&#x200B;**CusIndividual**、列に&#x200B;**lastName**&#x200B;および&#x200B;**firstName**&#x200B;を使用していました。

スキーマでは、既存のテーブルの列の一部のみを入力できます。 未入力の列にはユーザーはアクセスできません。

## 索引付きフィールド {#indexed-fields}

クライアントコンソールからリストのレコードを並べ替えると、インデックス付きフィールドを並べ替えることで、パフォーマンスが向上します。 スキーマでインデックスを宣言すると、次に示すように、コンソールには列ラベルの左側にあるソート順の矢印の下に赤い線が付いたインデックス付きフィールドが表示されます。

![](assets/s_ncs_integration_mapping_index.png)

スキーマでは、インデックスは次のように定義されます。

```
<dbindex name="name_of_index" unique="true/false"
  <keyfield xpath="xpath_1st_field"/
  <keyfield xpath="xpath_2nd_field"/
  ...
</dbindex
```

そのため、一致するスキーマでカスタムテーブルの既存のインデックスを宣言することが重要です。

ソーススキーマの各キーとリンク宣言に対して、インデックスが暗黙的に宣言されます。 インデックス宣言は、**noDbIndex=&quot;true&quot;**&#x200B;属性を指定することで防ぐことができます。

**例**：

```
<key internal="true" name="customer" noDbIndex="true">
  <keyfield xpath="@customerId"/>
</key>
```
