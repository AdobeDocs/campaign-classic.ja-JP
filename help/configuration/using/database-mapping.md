---
product: campaign
title: データベースマッピング
description: データベースマッピング
feature: Configuration, Instance Settings
role: Developer
exl-id: 728b509f-2755-48df-8b12-449b7044e317
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 46%

---

# データベースマッピング{#database-mapping}

[ このページで ](schema-structure.md) 説明されているサンプルスキーマの SQL マッピングにより、次の XML ドキュメントが生成されます。

```sql
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">
  <enumeration basetype="byte" name="gender">    
    <value label="Not specified" name="unknown" value="0"/>    
    <value label="Male" name="male" value="1"/>    
    <value label="Female" name="female" value="2"/> 
  </enumeration>  

  <element name="recipient" sqltable="CusRecipient">    
    <attribute desc="Recipient email address" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>    
    <attribute default="GetDate()" label="Date of creation" name="created" sqlname="tsCreated" type="datetime"/>    
    <attribute enum="gender" label="Gender" name="gender" sqlname="iGender" type="byte"/>    
    <element label="Location" name="location">      
      <attribute label="City" length="50" name="city" sqlname="sCity" type="string" userEnum="city"/>    
    </element>  
  </element>
</schema>
```

スキーマのルート要素が **`<srcschema>`** から **`<schema>`** に変更されました。

この他のタイプのドキュメントは、ソーススキーマから自動的に生成され、単にスキーマと呼ばれます。

SQL 名は、要素名と型に基づいて自動的に決定されます。

SQL の命名規則は次のとおりです。

* **table**：スキーマの名前空間と名前を連結したもの

  この例では、テーブルの名前は、スキーマのメイン要素を使用して **sqltable** 属性に入力されます。

  ```sql
  <element name="recipient" sqltable="CusRecipient">
  ```

* **field**：型に従って定義されたプレフィックスが先頭に付く要素名：整数の場合は「i」、倍精度数の場合は「d」、文字列の場合は「s」、日付の場合は「ts」など。

  フィールド名は、型指定された **`<attribute>`** および **`<element>`** ごとに **sqlname** 属性を使用し入力されます。

  ```sql
  <attribute desc="Email address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/> 
  ```

>[!NOTE]
>
>SQL 名は、ソーススキーマからオーバーロードできます。それには、関係する要素の「sqltable」または「sqlname」属性を設定します。

拡張スキーマから生成されるテーブルを作成する SQL スクリプトは、次のとおりです。

```sql
CREATE TABLE CusRecipient(
  iGender NUMERIC(3) NOT NULL Default 0,   
  sCity VARCHAR(50),   
  sEmail VARCHAR(80),
  tsCreated TIMESTAMP Default NULL);
```

SQL フィールドの制約は次のとおりです。

* 数値フィールドと日付フィールドに null 値はありません
* 数値フィールドは 0 に初期化されます

## XML フィールド {#xml-fields}

デフォルトでは、**`<attribute>`** および **`<element>`** で型指定された要素は、データスキーマテーブルの SQL フィールドにマッピングされます。 ただし、このフィールドを SQL ではなく XML で参照することができます。つまり、データは、すべての XML フィールドの値を含んだテーブルのメモフィールド（「mData」）に格納されます。これらのデータのストレージは、スキーマ構造に準拠する XML ドキュメントです。

XML のフィールドにデータを入力するには、値「true」の **xml** 属性を、該当する要素に追加する必要があります。

**例**：XML フィールドの使用例を 2 つ示します。

* 複数行コメントフィールド：

  ```sql
  <element name="comment" xml="true" type="memo" label="Comment"/>
  ```

* HTML 形式でのデータの説明：

  ```sql
  <element name="description" xml="true" type="html" label="Description"/>
  ```

  「html」タイプを使用すると、HTML コンテンツを CDATA タグに格納し、Adobe Campaign クライアントインターフェイスに特別な HTML 編集チェックを表示できます。

XML フィールドを使用すると、データベースの物理構造を変更せずに新しいフィールドを追加できます。 もう 1 つの利点は、使用するリソースが少ないことです（SQL フィールドに割り当てるサイズ、テーブルあたりのフィールド数の制限など）。 ただし、XML フィールドのインデックス作成やフィルタリングは行えません。

## インデックス付きフィールド {#indexed-fields}

インデックスを使用すると、アプリケーションで使用される SQL クエリのパフォーマンスを最適化できます。

インデックスは、データスキーマのメイン要素から宣言されます。

```sql
<dbindex name="name_of_index" unique="true/false">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

インデックスは次のルールに従います。

* インデックスでは、テーブル内の 1 つ以上のフィールドを参照できます
* **unique** 属性に「true」という値が含まれている場合、すべてのフィールドで（重複を避けるために）インデックスを一意にすることができます
* インデックスの SQL 名は、テーブルの SQL 名とインデックスの名前から決定されます

>[!NOTE]
>
>* 原則として、インデックスは、スキーマのメイン要素から宣言される最初の要素です。
>
>* インデックスは、テーブルマッピング（標準または FDA）の際に自動的に作成されます。

**例**：

* メールアドレスと市区町村へのインデックスの追加：

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

* 「id」名フィールドに一意のインデックスを追加します。

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

詳しくは、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [スキーマの構造](schema-structure.md)
* [鍵の管理](database-keys.md)
* [リンク管理](database-links.md)
* [Campaign データモデル](about-data-model.md)