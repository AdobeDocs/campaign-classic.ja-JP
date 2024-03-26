---
product: campaign
title: スキーマエディションの例
description: スキーマエディションの例
feature: Schema Extension
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: b7ee70e0-89c6-4cd3-8116-2f073d4a2f2f
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---


# スキーマエディションの例{#examples-of-schemas-edition}

## テーブルの拡張 {#extending-a-table}

を拡張するには、以下を実行します。 **nms:recipient** スキーマ受信者テーブルに、以下の手順を適用します。

1. 拡張スキーマ (**cus:extension**) を次のデータで使用します。

   ```
   <srcSchema mappingType="sql" name="extension" namespace="cus" xtkschema="xtk:srcSchema" extendedSchema="nms:recipient">  
     <enumeration basetype="string" default="area1" name="area">    
       <value label="Zone 1" name="area1"/>    
       <value label="Zone 2" name="area2"/>  
     </enumeration>  
   
     <element name="extension">    
       <dbindex name="area">      
         <keyfield xpath="location/@area"/>    
       </dbindex>      
   
       <attribute label="Loyalty code" name="fidelity" type="long"/>    
       <element name="location">      
         <attribute name="area" label="Purchasing zone" type="string" length="50" enum="area"/>    
       </element>  </element>  
   </srcSchema>
   ```

   この例では、インデックス付きのフィールド (**忠実さ**) が追加され、 **場所** ( 既に **nms:recipient** スキーマ ) は、列挙されたフィールド (**領域**) をクリックします。

   >[!IMPORTANT]
   >
   >必ず **extendedSchema** 拡張スキーマを参照する属性。

1. 拡張スキーマが **nms:recipient** スキーマを作成し、追加データが存在することを示します。

   ```
   <schema dependingSchemas="cus:extension" mappingType="sql" name="recipient" namespace="nms" xtkschema="xtk:schema">
     ...
     <enumeration basetype="string" default="area1" name="area">    
       <value label="Zone 1" name="area1"/>    
       <value label="Zone 2" name="area2"/>  
     </enumeration>
     ...
     <element autopk="true" name="recipient" sqltable="NmsRecipient"> 
       <dbindex name="area">      
         <keyfield xpath="location/@area"/>    
       </dbindex>
   
       ...
       <attribute belongsTo="cus:extension" label="Loyalty code" name="fidelity" sqlname="iFidelity" type="long"/>
       <element name="location">
         ...
         <attribute enum="area" label="Purchasing zone" length="50" name="area" sqlname="sArea" type="string"/>
       </element>
       ...
     </element>
   </schema>
   ```

   データベース更新ウィザードから生成される SQL スクリプトは次のとおりです。

   ```
   ALTER TABLE NmsRecipient ADD iFidelity INTEGER;
   UPDATE NmsRecipient SET iFidelity = 0;
   ALTER TABLE NmsRecipient ALTER COLUMN iFidelity SET NOT NULL;ALTER TABLE NmsRecipient ALTER COLUMN iFidelity SET Default 0;
   ALTER TABLE NmsRecipient ADD sArea VARCHAR(50); 
   CREATE INDEX NmsRecipient_area ON NmsRecipient(sArea);
   ```

## リンクされたコレクションテーブル {#linked-collection-table}

この項では、基数が 1-N の受信者テーブルにリンクされた注文テーブルを作成する方法について説明します。

オーダーテーブルのソーススキーマ：

```
<srcSchema label="Order" name="order" namespace="cus" xtkschema="xtk:srcSchema">  
  <element autopk="true" name="order">    
    <compute-string expr="@number" + '(' + ToString(@date) + ')'/>    
    
    <attribute label="Number" length="128" name="number" type="string"/>    
    <attribute desc="Order date" label="Date" name="date" type="datetime" default="GetDate()"/>    
    <attribute desc="order total" label="Total" name="total" type="double"/>    
    <element label="Recipient" name="recipient" revDesc="Orders associated with this recipient" revIntegrity="own" revLabel="Orders" target="nms:recipient" type="link"/>  
  </element>
</srcSchema>
```

テーブルのタイプは、 **自動車** 受信者テーブルへのリンクの結合で使用する自動生成プライマリキーを作成するために使用します。

生成されたスキーマ：

```
<schema label="Order" mappingType="sql" name="order" namespace="cus" xtkschema="xtk:schema">  
  <element autopk="true" label="Order" name="order" sqltable="CusOrder">    
    <compute-string expr="ToString(@date) + ' - ' + @number"/>    

    <dbindex name="id" unique="true">      
      <keyfield xpath="@id"/>    
    </dbindex>    

    <key internal="true" name="id">      
      <keyfield xpath="@id"/>    
    </key>    

    <dbindex name="recipientId">      
      <keyfield xpath="@recipient-id"/>    
    </dbindex>    

    <attribute desc="Internal primary key" label="Primary key" name="id" sqlname="iOrderId" type="long"/>    
    <attribute label="Number" length="128" name="number" sqlname="sNumber" type="string"/>    
    <attribute desc="Order date" label="Date" name="date" sqlname="tsDate" type="datetime"/>    
    <attribute desc="order total" label="Total" name="total" sqlname="Total" type="double"/>    
    <element label="Recipient" name="recipient" revLink="order" target="nms:recipient" type="link">      
      <join xpath-dst="@id" xpath-src="@recipient-id"/>    
    </element>    
    <attribute advanced="true" label="Foreign key of 'Recipient' link ('id' field)" name="recipient-id" sqlname="iRecipientId" type="long"/>  
   </element>
</schema>
```

テーブル作成 SQL スクリプトは、次のとおりです。

```
CREATE TABLE CusOrder(dTotal DOUBLE PRECISION NOT NULL Default 0, iOrderId INTEGER NOT NULL Default 0, iRecipientId INTEGER NOT NULL Default 0, sNumber VARCHAR(128), tsDate TIMESTAMP Default NULL);
CREATE UNIQUE INDEX CusOrder_id ON CusOrder(iOrderId);
CREATE INDEX CusOrder_recipientId ON CusOrder(iRecipientId);  
INSERT INTO CusOrder (iOrderId) VALUES (0); 
```

>[!NOTE]
>
>スクリプトの最後に INSERT INTO コマンドを使用すると、0 に設定された識別子レコードを挿入して、外部結合をシミュレートできます。

## 拡張テーブル {#extension-table}

拡張テーブルを使用すると、基数 1-1 のリンクされたテーブル内の既存のテーブルのコンテンツを拡張できます。

拡張テーブルの目的は、テーブルでサポートされるフィールドの数に制限がないようにするか、オンデマンドで消費されるデータの占有領域を最適化することです。

拡張テーブルスキーマの作成 (**cus:feature**):

```
<srcSchema mappingType="sql" name="feature" namespace="cus" xtkschema="xtk:srcSchema">  
  <element autopk="true" name="feature">    
    <attribute label="Children" name="children" type="byte"/>    
    <attribute label="Single" name="single" type="boolean"/>    
    <attribute label="Spouse first name" length="100" name="spouseFirstName" type="string"/>  
  </element>
</srcSchema>
```

カーディナリティ 1-1 のリンクを追加する、受信者テーブルに拡張スキーマを作成する：

```
<srcSchema extendedSchema="nms:recipient" label="Recipient" mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:srcSchema">  
  <element name="recipient">    
    <element desc="Features" integrity="own" label="Features" name="feature" revCardinality="single" revLink="recipient" target="cus:feature" type="link"/> 
  </element>
</srcSchema>
```

>[!NOTE]
>
>受信者テーブルと拡張テーブルの間のリンクの定義は、外部キーを含むスキーマから入力する必要があります。

拡張テーブルを作成するための SQL スクリプトを次に示します。

```
CREATE TABLE CusFeature(  iChildren NUMERIC(3) NOT NULL Default 0, iFeatureId INTEGER NOT NULL Default 0, iSingle NUMERIC(3) NOT NULL Default 0, sSpouseFirstName VARCHAR(100));
CREATE UNIQUE INDEX CusFeature_id ON CusFeature(iFeatureId);  
INSERT INTO CusFeature (iFeatureId) VALUES (0); 
```

受信者テーブルの SQL 更新スクリプトは、次のとおりです。

```
ALTER TABLE NmsRecipient ADD iFeatureId INTEGER;
UPDATE NmsRecipient SET iFeatureId = 0;
ALTER TABLE NmsRecipient ALTER COLUMN iFeatureId SET NOT NULL;
ALTER TABLE NmsRecipient ALTER COLUMN iFeatureId SET Default 0;
CREATE INDEX NmsRecipient_featureId ON NmsRecipient(iFeatureId);
```

## オーバーフローテーブル {#overflow-table}

オーバーフローテーブルは拡張テーブル（カーディナリティ 1-1）ですが、拡張するテーブルへのリンクの宣言は、オーバーフローテーブルのスキーマに入力されます。

オーバーフローテーブルには、拡張するテーブルの外部キーが含まれます。 したがって、拡張するテーブルは変更されません。 2 つのテーブル間の関係は、拡張するテーブルのプライマリキーの値です。

オーバーフローテーブルスキーマ (**cus:overflow**):

```
<srcSchema label="Overflow" name="overflow" namespace="cus" xtkschema="xtk:srcSchema">  
  <element name="overflow">    
    <key internal="true" name="id">      
      <keyfield xlink="recipient"/>    
    </key>    

    <attribute label="Children" name="children" type="byte"/>    
    <attribute label="Single" name="single" type="boolean"/>    
    <attribute label="Spouse first name" length="100" name="spouseFirstName" type="string"/>  
    <element label="Customer" name="recipient" revCardinality="single" revIntegrity="own" revExternalJoin="true" target="nms:recipient" type="link"/>  
  </element>  
</srcSchema>
```

>[!NOTE]
>
>オーバーフローテーブルのプライマリキーは、拡張するテーブルへのリンクです（この例では「nms:recipient」スキーマ）。

テーブル作成 SQL スクリプトは、次のとおりです。

```
CREATE TABLE CusOverflow(iChildren NUMERIC(3) NOT NULL Default 0, iRecipientId INTEGER NOT NULL Default 0, iSingle NUMERIC(3) NOT NULL Default 0, sSpouseFirstName VARCHAR(100));
CREATE UNIQUE INDEX CusOverflow2_id ON CusOverflow2(iRecipientId);  
```

## 関係テーブル {#relationship-table}

関係テーブルを使用すると、2 つのテーブルを基数 N ～ N にリンクできます。このテーブルには、リンクするテーブルの外部キーのみが含まれています。

グループ間の関係テーブル (**nms:group**) および受信者 (**nms:recipient**) をクリックします。

関係テーブルのソーススキーマ：

```
<srcSchema name="rcpGrpRel" namespace="cus">
  <element name="rcpGrpRel">
    <key internal="true" name="id">      
      <keyfield xlink="rcpGroup"/>      
      <keyfield xlink="recipient"/>    
    </key>

    <element integrity="neutral" label="Recipient" name="recipient" revDesc="Groups to which this recipient belongs" revIntegrity="own" revLabel="Groups" target="nms:recipient" type="link"/>    
    <element integrity="neutral" label="Group" name="rcpGroup" revDesc="Recipients in the group" revIntegrity="own" revLabel="Recipients" revLink="rcpGrpRel" target="nms:group" type="link"/>
  </element>
</srcSchema>
```

生成されるスキーマは次のとおりです。

```
<schema mappingType="sql" name="rcpGrpRel" namespace="cus" xtkschema="xtk:schema">  
  <element name="rcpGrpRel" sqltable="CusRcpGrpRel">    
    <compute-string expr="ToString([@rcpGroup-id]) + ',' + ToString([@recipient-id])"/>    
    <dbindex name="id" unique="true">      
      <keyfield xpath="@rcpGroup-id"/>      
      <keyfield xpath="@recipient-id"/>    
    </dbindex>    

    <key internal="true" name="id">      
      <keyfield xpath="@rcpGroup-id"/>      
      <keyfield xpath="@recipient-id"/>    
    </key>    

    <dbindex name="rcpGroupId">      
      <keyfield xpath="@rcpGroup-id"/>    
    </dbindex>    
    <dbindex name="recipientId">      
      <keyfield xpath="@recipient-id"/>    
    </dbindex>    

    <element integrity="neutral" label="Recipient" name="recipient" revLink="rcpGrpRel" target="nms:recipient" type="link">      
      <join xpath-dst="@id" xpath-src="@recipient-id"/>    
    </element>    
    <attribute advanced="true" label="Foreign key of 'Recipient' link ('id' field)" name="recipient-id" sqlname="iRecipientId" type="long"/>    

    <element integrity="neutral" label="Group" name="rcpGroup" revLink="rcpGrpRel" target="nms:group" type="link">      
      <join xpath-dst="@id" xpath-src="@rcpGroup-id"/>    
    </element>    
    <attribute advanced="true" label="Foreign key of 'Group' link ('id' field)" name="rcpGroup-id" sqlname="iRcpGroupId" type="long"/>  
  </element>
</schema>
```

テーブル作成 SQL スクリプトは、次のとおりです。

```
CREATE TABLE CusRcpGrpRel( iRcpGroupId INTEGER NOT NULL Default 0, iRecipientId INTEGER NOT NULL Default 0);
CREATE UNIQUE INDEX CusRcpGrpRel_id ON CusRcpGrpRel(iRcpGroupId, iRecipientId);
CREATE INDEX CusRcpGrpRel_recipientId ON CusRcpGrpRel(iRecipientId);
```

## 使用例：フィールドを既存の参照テーブルにリンクする {#uc-link}

この使用例では、既存の参照テーブルを、組み込みのAdobe Campaign列挙メカニズム (enum、userEnum、dbEnum) の代わりに使用する方法を示します。

既存の参照テーブルをスキーマの列挙として使用することもできます。 これは、テーブルと参照テーブルの間にリンクを作成し、属性を追加することで実現できます **displayAsField=&quot;true&quot;**.

この例では、参照テーブルに銀行名と識別子のリストが含まれています。

```
<srcSchema entitySchema="xtk:srcSchema" img="cus:bank16x16.png" label="Bank" mappingType="sql" name="bank" namespace="cus"
xtkschema="xtk:srcSchema">
    <element img="cus:bank16x16.png" label="Banks" name="bank">
        <compute-string expr="@name"/>
        <key name="id">
            <keyfield xpath="@id"/>
        </key>
        <attribute label="Bank Id" name="id" type="short"/>
        <attribute label="Name" length="64" name="name" type="string"/>
     </element> 
</srcSchema>
```

この参照テーブルを使用する任意のテーブルで、リンクを定義し、 **displayAsField=&quot;true&quot;** 属性。

```
<element displayAsField="true" label="Bank" name="bank" target="cus:bank" type="link" noDbIndex="true"/>
```

ユーザーインターフェイスにはリンクではなくフィールドが表示されます。 ユーザがそのフィールドを選択すると、参照テーブルから値を選択するか、オートコンプリート機能を使用できます。

![](assets/schema-edition-ex.png)

* オートコンプリートをおこなうには、参照テーブルで計算文字列を定義する必要があります。

* 次を追加： **noDbIndex=&quot;true&quot;** 属性を使用して、Adobe Campaignがリンクのソーステーブルに格納された値にインデックスを作成できないようにします。

## 関連トピック

* [列挙の操作](../../platform/using/managing-enumerations.md)

* [Campaign スキーマの概要](../../configuration/using/about-schema-edition.md)

* [データベース構造の更新](../../configuration/using/updating-the-database-structure.md)
