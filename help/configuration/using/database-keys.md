---
product: campaign
title: データスキーマでの鍵の管理
description: データスキーマでの鍵管理の理解
feature: Configuration, Instance Settings
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
source-git-commit: 46220dcfdddb8f6f1e7026cafc503aaeecb7e0fa
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 23%

---


# スキーマでの鍵の管理 {#management-of-keys}

データスキーマに関連付けられた各テーブルには、テーブル内のレコードを識別するためのキーが少なくとも 1 つ必要です。

キーがデータスキーマのメイン要素から宣言されます。

```sql
<key name="name_of_key">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

キーが入力されるスキーマ内の最初のキーである場合、またはキーに `internal` 属性が「true」に設定されている場合にのみ有効です。


次のルールがキーに適用されます。

* キーは、テーブル内の 1 つ以上のフィールドを参照できます
* 一意のインデックスは、各キー定義に対して暗黙的に宣言されます。 キーにインデックスを作成するのを防ぐには、 `noDbIndex` 属性を「true」に設定します。

>[!NOTE]
>
>* 標準として、キーは、インデックスが定義された後に、スキーマのメイン要素から宣言された要素です。
>
>* テーブルマッピング中にキーが作成（標準または FDA）、Adobe Campaignは一意のインデックスを検索します。

**例**：

* E メールアドレスと市区町村にキーを追加する：

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

ほとんどのAdobe Campaignテーブルのプライマリキーは、データベースエンジンによって自動生成される 32 ビット長の整数です。 キー値の計算はシーケンスに依存します ( デフォルトでは、 **XtkNewId** SQL 関数 ) を使用して、データベース全体で一意の数値を生成します。 レコードの挿入時に、キーの内容が自動的に入力されます。

増分キーの利点は、テーブル間の結合に対して変更不可のテクニカルキーを提供することです。 また、このキーは 2 バイトの整数を使用するので、メモリを多く使用しません。

ソーススキーマで、 **pkSequence** 属性。 この属性がソーススキーマで指定されていない場合、 **XtkNewId** デフォルトのシーケンスが使用されます。 アプリケーションは、 **nms:broadLog** および **nms:trackingLog** スキーマ (**NmsBroadLogId** および **NmsTrackingLogId** それぞれ ) を確認します。

ACC 18.10 以降、 **XtkNewId** は、標準スキーマのシーケンスのデフォルト値ではなくなりました。 これで、スキーマを構築したり、専用のシーケンスで既存のスキーマを拡張したりできるようになりました。

>[!IMPORTANT]
>
>スキーマを新しく作成するときや、スキーマを拡張するときは、スキーマ全体で同じプライマリキーのシーケンス値（@pkSequence）を保持する必要があります。

Adobe Campaignスキーマで参照されるシーケンス (**NmsTrackingLogId** 例えば、) は、パラメーター内の ID の数をコンマで区切って返す SQL 関数に関連付ける必要があります。 この関数は、呼び出す必要があります **GetNew** XXX **Ids**&#x200B;です。 **XXX** はシーケンスの名前 (**GetNewNmsTrackingLogIds** 例えば )。 次を表示： **postgres-nms.sql**, **mssql-nms.sql** または **oracle-nms.sql** アプリケーションで指定されたファイル ( **datakit/nms/eng/sql/** 各データベースエンジンの「NmsTrackingLogId」シーケンス作成の例を復元するディレクトリ。

一意のキーを宣言するには、 **自動車** データスキーマのメイン要素の属性（値が「true」）。

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