---
product: campaign
title: データスキーマにおける鍵の管理
description: データスキーマでのキー管理について
feature: Configuration, Instance Settings
role: Data Engineer, Developer
exl-id: faf63c8f-9d10-43c1-a990-91361594af9f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 30%

---

# スキーマでのキー管理 {#management-of-keys}

データスキーマに関連付けられた各テーブルには、テーブル内のレコードを識別するためのキーが少なくとも 1 つ必要です。

キーがデータスキーマのメイン要素から宣言されます。

```sql
<key name="name_of_key">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

キーがスキーマ内で最初に入力される場合や、「true」に設定された `internal` 属性を含む場合、そのキーは「プライマリキー」と呼ばれます。

キーには次のルールが適用されます。

* キーは、テーブル内の 1 つ以上のフィールドを参照できます
* 一意のインデックスは、各キー定義に対して暗黙的に宣言されます。 キーのインデックスの作成は、`noDbIndex` 属性を「true」に設定することで防ぐことができます。

>[!NOTE]
>
>* 標準的に、キーとは、インデックスが定義された後にスキーマのメイン要素から宣言される要素です。
>
>* キーはテーブルマッピング（標準または FDA）中に作成され、Adobe Campaignは一意のインデックスを見つけます。

**例**：

* メールアドレスと市区町村へのキーの追加：

  ```sql
  <srcSchema name="recipient" namespace="cus">
    <element name="recipient">
      <key name="email">
        <keyfield xpath="@email"/> 
        <keyfield xpath="location/@city"/> 
      </key>
  
      <attribute name="email" type="string" length="80" label="Email" desc="Email address of recipient"/>
      <element name="location" label="Location">
        <attribute name="city" type="string" length="50" label="City" userEnum="city"/>
      </element>
    </element>
  </srcSchema>
  ```

  生成されたスキーマ：

  ```sql
  <schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
    <element name="recipient" sqltable="CusRecipient">    
     <dbindex name="email" unique="true">      
       <keyfield xpath="@email"/>      
       <keyfield xpath="location/@city"/>    
     </dbindex>    
  
     <key name="email">      
      <keyfield xpath="@email"/>      
      <keyfield xpath="location/@city"/>    
     </key>    
  
     <attribute desc="Email address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>    
     <element label="Location" name="location">      
       <attribute label="City" length="50" name="city" sqlname="sCity" type="string" userEnum="city"/>    
     </element>  
    </element>
  </schema>
  ```

* 「id」名フィールドへのプライマリキーまたは内部キーの追加：

  ```sql
  <srcSchema name="recipient" namespace="cus">
    <element name="recipient">
      <key name="id" internal="true">
        <keyfield xpath="@id"/> 
      </key>
  
      <key name="email" noDbIndex="true">
        <keyfield xpath="@email"/> 
      </key>
  
      <attribute name="id" type="long" label="Identifier"/>
      <attribute name="email" type="string" length="80" label="Email" desc="Email address of recipient"/>
    </element>
  </srcSchema>
  ```

  生成されたスキーマ：

  ```sql
  <schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
    <element name="recipient" sqltable="CusRecipient">    
      <key name="email">      
        <keyfield xpath="@email"/>    
      </key>    
  
      <dbindex name="id" unique="true">      
        <keyfield xpath="@id"/>    
      </dbindex>    
  
      <key internal="true" name="id">      
       <keyfield xpath="@id"/>    
      </key>    
  
      <attribute label="Identifier" name="id" sqlname="iRecipientId" type="long"/>    
      <attribute desc="Email address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>  
    </element>
  </schema>
  ```

## 自動増分キー {#auto-incremental-key}

ほとんどのAdobe Campaign テーブルのプライマリキーは、データベースエンジンによって自動生成される 32 ビットの長い整数です。 キー値の計算は、データベース全体で一意の数値を生成するシーケンス （デフォルトでは **XtkNewId** SQL 関数）によって異なります。 レコードの挿入時に、キーの内容が自動的に入力されます。

増分キーの利点は、テーブル間の結合に変更不可能なテクニカルキーを提供することです。 さらに、このキーは 2 バイトの整数を使用するので、多くのメモリを占有しません。

ソーススキーマで、**pkSequence** 属性で使用するシーケンスの名前を指定できます。 この属性がソーススキーマで指定されていない場合は、デフォルトのシーケンス **XtkNewId** が使用されます。 **nms:broadLog** および **nms:trackingLog** スキーマ（それぞれ **NmsBroadLogId** および **NmsTrackingLogId**）は、レコード数が最も多いテーブルであるため、アプリケーションでは専用のシーケンスを使用します。

ACC 18.10 以降、**XtkNewId** は、標準スキーマのシーケンスのデフォルト値ではなくなりました。 これで、専用のシーケンスでスキーマを構築したり、既存のスキーマを拡張したりできるようになりました。

>[!IMPORTANT]
>
>スキーマを新しく作成するときや、スキーマを拡張するときは、スキーマ全体で同じプライマリキーのシーケンス値（@pkSequence）を保持する必要があります。

Adobe Campaign スキーマで参照されているシーケンス（**NmsTrackingLogId** など）は、パラメーター内の ID の数をコンマで区切って返す SQL 関数に関連付ける必要があります。 この関数は、**GetNew** XXX **Ids** と呼ぶ必要があります。**XXX** は、シーケンスの名前です（例：**GetNewNmsTrackingLogIds**）。 アプリケーションに付属の **postgres-nms.sql**、**mssql-nms.sql** または **datakit/nms/eng/sql/** ディレクトリにあるoracle-nms.sql **ファイルを表示し、各データベースエンジンの「NmsTrackingLogId」シーケンス作成の例を復元します**。

一意のキーを宣言するには、データスキーマのメイン要素の **autopk** 属性（値「true」）に入力します。

**例**：

ソーススキーマでの増分キーの宣言：

```sql
<srcSchema name="recipient" namespace="cus">
  <element name="recipient" autopk="true">
  ...
  </element>
</srcSchema>
```

生成されたスキーマ：

```sql
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
  <element name="recipient" autopk="true" pkSequence="XtkNewId" sqltable="CusRecipient"> 
    <dbindex name="id" unique="true">
      <keyfield xpath="@id"/>
    </dbindex>

    <key internal="true" name="id">
      <keyfield xpath="@id"/>
    </key>

    <attribute desc="Internal primary key" label="Primary key" name="id" sqlname="iRecipientId" type="long"/>
  </element>
</schema>
```

キーとそのインデックスの定義に加えて、自動生成されたプライマリキーを格納するために、「id」と呼ばれる数値フィールドが拡張スキーマに追加されました。

>[!IMPORTANT]
>
>プライマリキーが 0 に設定されたレコードは、テーブルの作成時に自動的に挿入されます。このレコードは、外部結合を避けるために使用されます。外部結合はボリュームテーブルでは有効ではありません。デフォルトでは、外部キーはすべて値 0 で初期化されるので、データ項目が入力されていない場合でも常に、結合時に結果を返します。


## 詳細情報

詳しくは、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [スキーマの構造](schema-structure.md)
* [データベースマッピング](database-mapping.md)
* [リンク管理](database-links.md)
* [Campaign データモデル](about-data-model.md)
