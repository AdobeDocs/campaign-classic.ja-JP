---
solution: Campaign Classic
product: campaign
title: データスキーマ
description: データスキーマ
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---


# データスキーマ{#data-schemas}

## 原則 {#principles}

スキーマを編集、作成および設定するには、Adobe Campaignクライアントコンソールの&#x200B;**[!UICONTROL 管理/設定/データスキーマ]**&#x200B;ノードをクリックします。

>[!NOTE]
>
>そのまま使用できるデータスキーマは、Adobe Campaign Classicコンソールの管理者のみが削除できます。

![](assets/d_ncs_integration_schema_navtree.png)

編集フィールドには、ソーススキーマのXMLコンテンツが表示されます。

![](assets/d_ncs_integration_schema_edition.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるスキーマキーを入力できます。 スキーマのルート要素の「name」属性と「名前空間」属性は、スキーマのXML編集ゾーンで自動的に更新されます。

プレビューは、拡張スキーマを自動的に生成します。

![](assets/d_ncs_integration_schema_edition2.png)

>[!NOTE]
>
>ソーススキーマを保存すると、拡張スキーマの生成が自動的に開始されます。

スキーマの完全な構造を確認する必要がある場合は、「プレビュー」タブを使用できます。 スキーマを拡張すると、そのすべての拡張を視覚化できます。 補完的に、「ドキュメント」タブには、すべてのスキーマ属性と要素、およびそのプロパティ（SQLフィールド、タイプ/長さ、ラベル、説明）が表示されます。 「ドキュメント」タブは、生成されたスキーマにのみ適用されます。 詳しくは、「[スキーマの再生成](../../configuration/using/regenerating-schemas.md)」を参照してください。

## 例：契約表の作成{#example--creating-a-contract-table}

次の例では、Adobe Campaignデータベースのデータベースモデルに&#x200B;**contracts**&#x200B;の新しいテーブルを作成します。 次の表に、各契約の所有者および共有者の姓と名と電子メールアドレスを格納します。

これを行うには、テーブルのスキーマを作成し、対応するテーブルを生成するためにデータベース構造を更新する必要があります。 次のような流れになります。

1. Adobe Campaignツリーの&#x200B;**[!UICONTROL 管理/設定/データスキーマ]**&#x200B;ノードを編集し、**[!UICONTROL 新規]**&#x200B;をクリックします。
1. 「**[!UICONTROL データモデルに新しいテーブルを作成]**」オプションを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_configuration_create_new_schema.png)

1. テーブル名と名前空間を指定します。

   ![](assets/s_ncs_configuration_create_new_param.png)

   >[!NOTE]
   >
   >デフォルトでは、ユーザーが作成したスキーマは「cus」名前空間に保存されます。 詳しくは、[スキーマのID](../../configuration/using/about-schema-reference.md#identification-of-a-schema)を参照してください。

1. テーブルのコンテンツを作成します。 設定が足りないことを確認するために、入力ウィザードを使用することをお勧めします。 これを行うには、「**[!UICONTROL 挿入]**」ボタンをクリックし、追加する設定のタイプを選択します。

   ![](assets/s_ncs_configuration_create_new_content.png)

1. 契約表の設定を定義します。

   ```
   <srcSchema desc="Active contracts" img="ncm:channels.png" label="Contracts" labelSingular="Contract" mappingType="sql" name="Contracts" namespace="cus" xtkschema="xtk:srcSchema">
     <element desc="Active contracts" img="ncm:channels.png" label="Contracts" labelSingular="Contract"
              name="Contracts" autopk="true">
              <attribute name="holderName" label="Holder last name" type="string"/>
              <attribute name="holderFirstName" label="Holder first name" type="string"/>
              <attribute name="holderEmail" label="Holder email" type="string"/>
              <attribute name="co-holderName" label="Co-holder last name" type="string"/>           
              <attribute name="co-holderFirstName" label="Co-holder first name" type="string"/>           
              <attribute name="co-holderEmail" label="Co-holder email" type="string"/>    
              <attribute name="date" label="Subscription date" type="date"/>     
              <attribute name="noContract" label="Contract number" type="long"/>  
     </element>
   </srcSchema>
   ```

   契約追加の種類と、契約番号にインデックスを付けます。

   ```
   <srcSchema _cs="Contracts (cus)" desc="Active contracts" entitySchema="xtk:srcSchema" img="ncm:channels.png"
              label="Contracts" labelSingular="Contract" name="Contracts" namespace="cus" xtkschema="xtk:srcSchema">
     <enumeration basetype="byte" name="typeContract">
       <value label="Home" name="home" value="0"/>
       <value label="Car" name="car" value="1"/>
       <value label="Health" name="health" value="2"/>
       <value label="Pension fund" name="pension fund" value="2"/>
     </enumeration>
     <element autopk="true" desc="Active contracts" img="ncm:channels.png" label="Contracts"
              labelSingular="Contract" name="Contracts">
       <attribute label="Holder last name" name="holderName" type="string"/>
       <attribute label="Holder first name" name="holderFirstName" type="string"/>
       <attribute label="Holder email" name="holderEmail" type="string"/>
       <attribute label="Co-holder last name" name="co-holderName" type="string"/>
       <attribute label="Co-holder first name" name="co-holderFirstName" type="string"/>
       <attribute label="Co-holder email" name="co-holderEmail" type="string"/>
       <attribute label="Subscription date" name="date" type="date"/>
      <attribute desc="Type of contract" enum="cus:Contracts:typeContract" label="Type of contract"
                  name="type" type="byte"/>
       <attribute label="Contract number" name="noContract" type="long"/>
       <dbindex name="noContract" unique="true">
         <keyfield xpath="@noContract"/>
       </dbindex>
     </element>
   </srcSchema>
   ```

1. スキーマを保存して構造を生成します。

   ![](assets/s_ncs_configuration_structure.png)

1. データベース構造を更新して、スキーマがリンクされるテーブルを作成します。 詳しくは、[データベース構造の更新](../../configuration/using/updating-the-database-structure.md)を参照してください。

