---
product: campaign
title: データスキーマでのキー管理
description: データスキーマのキー管理について
feature: Configuration, Instance Settings
role: Developer
exl-id: faf63c8f-9d10-43c1-a990-91361594af9f
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '627'
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

キーには、次のルールが適用されます。

* キーは、テーブルの1つ以上のフィールドを参照できます
* 各キー定義に対して、一意のインデックスが暗黙的に宣言されます。 キーにインデックスを作成しないようにするには、`noDbIndex`属性を「true」に設定します。

>[!NOTE]
>
>* 標準として、キーは、インデックスが定義された後にスキーマのメイン要素から宣言された要素です。
>
>* キーはテーブルマッピング（標準またはFDA）中に作成され、Adobe Campaignは一意のインデックスを見つけます。

**例**：

* 電子メールアドレスと都市にキーを追加する：

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

## 自動インクリメンタルキー {#auto-incremental-key}

ほとんどのAdobe Campaign テーブルの主キーは、データベースエンジンによって自動生成される32 ビットの長い整数です。 キー値の計算は、データベース全体で一意の数値を生成するシーケンス（デフォルトでは&#x200B;**XtkNewId** SQL関数）によって異なります。 キーの内容は、レコードの挿入時に自動的に入力されます。

増分キーの利点は、テーブル間の結合に変更不可能なテクニカルキーを提供できることです。 さらに、このキーは2 バイトの整数を使用するため、メモリをあまり消費しません。

ソーススキーマで、**pkSequence**&#x200B;属性で使用するシーケンスの名前を指定できます。 この属性がソーススキーマで指定されていない場合、**XtkNewId**&#x200B;のデフォルトシーケンスが使用されます。 このアプリケーションは、最も多くのレコードを含むテーブルであるため、**nms:broadLog**&#x200B;および&#x200B;**nms:trackingLog** スキーマ （**NmsBroadLogId**&#x200B;および&#x200B;**NmsTrackingLogId**）に専用シーケンスを使用します。

ACC 18.10以降、**XtkNewId**&#x200B;は、標準スキーマのシーケンスのデフォルト値ではなくなりました。 専用のシーケンスを使用して、スキーマを構築したり、既存のスキーマを拡張したりできるようになりました。

>[!IMPORTANT]
>
>スキーマを新しく作成するときや、スキーマを拡張するときは、スキーマ全体で同じプライマリキーのシーケンス値（@pkSequence）を保持する必要があります。

Adobe Campaign スキーマで参照されているシーケンス（**NmsTrackingLogId**&#x200B;など）は、パラメーター内のIDの数をコンマで区切って返すSQL関数に関連付ける必要があります。 この関数は&#x200B;**GetNew** XXX **Ids**&#x200B;と呼ぶ必要があります。ここで、**XXX**&#x200B;はシーケンスの名前です（**GetNewNmsTrackingLogIds**&#x200B;例）。 **datakit/nms/eng/sql/** ディレクトリのアプリケーションに付属している&#x200B;**postgres-nms.sql**、**mssql-nms.sql**&#x200B;または&#x200B;**oracle-nms.sql** ファイルを表示して、各データベースエンジンの「NmsTrackingLogId」シーケンス作成例を復元します。

一意のキーを宣言するには、データスキーマのメイン要素に&#x200B;**autopk**&#x200B;属性（値「true」）を入力します。

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

キーとそのインデックスの定義に加えて、自動生成されたプライマリキーを格納するために、「id」という数値フィールドが拡張スキーマに追加されました。

>[!IMPORTANT]
>
>プライマリキーが 0 に設定されたレコードは、テーブルの作成時に自動的に挿入されます。 このレコードは、外部結合を避けるために使用されます。外部結合はボリュームテーブルでは有効ではありません。 デフォルトでは、外部キーはすべて値 0 で初期化されるので、データ項目が入力されていない場合でも常に、結合時に結果を返します。


## 詳細情報

詳細については、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [スキーマの構造](schema-structure.md)
* [データベースマッピング](database-mapping.md)
* [リンク管理](database-links.md)
* [Campaign データモデル](about-data-model.md)
