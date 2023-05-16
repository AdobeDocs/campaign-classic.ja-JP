---
product: campaign
title: データスキーマ
description: Campaign データスキーマの概要
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Schema Extension
exl-id: d4446035-3988-4d89-b7df-7b8528c2e371
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 67%

---

# データスキーマ{#data-schemas}

## 原則 {#principles}

スキーマを編集、作成および設定するには、Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードをクリックします。

>[!NOTE]
>
>ビルトインデータスキーマは、Adobe Campaign Classic コンソールの管理者のみが削除できます。

![](assets/d_ncs_integration_schema_navtree.png)

編集フィールドに、ソーススキーマの XML コンテンツが表示されます。

![](assets/d_ncs_integration_schema_edition.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるスキーマキーを入力できます。 スキーマのルート要素の「name」属性と「namespace」属性は、スキーマの XML 編集ゾーンで自動的に更新されます。

プレビューは、拡張スキーマを自動的に生成します。

![](assets/d_ncs_integration_schema_edition2.png)

>[!NOTE]
>
>ソーススキーマを保存すると、拡張スキーマの生成が自動的に開始されます。

スキーマの構造を完全に確認する必要がある場合は、「プレビュー」タブを使用できます。 スキーマを拡張すると、そのすべての拡張を視覚化できます。 「ドキュメント」タブには、補足情報として、すべてのスキーマ属性と要素、およびそのプロパティ（SQL フィールド、タイプ／長さ、ラベル、説明）が表示されます。 「ドキュメント」タブは、生成されたスキーマにのみ適用されます。詳しくは、 [スキーマの再生成](../../configuration/using/regenerating-schemas.md) 」セクションに入力します。

## 例：契約テーブルの作成 {#example--creating-a-contract-table}

次の例では、用の新しいテーブルを作成します。 **契約** (Adobe Campaignデータベースのデータベースモデル )。 このテーブルには、契約ごとに、所有者と共同所有者の姓と名および E メールアドレスを格納できます。

それには、テーブルのスキーマを作成し、対応するテーブルを生成するためのデータベース構造を更新する必要があります。 次のような流れになります。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードを編集し、「**[!UICONTROL 新規]**」をクリックします。
1. を選択します。 **[!UICONTROL データモデルで新しいテーブルを作成する]** オプションを選択し、 **[!UICONTROL 次へ]** .

   ![](assets/s_ncs_configuration_create_new_schema.png)

1. テーブル名と名前空間を指定します。

   ![](assets/s_ncs_configuration_create_new_param.png)

   >[!NOTE]
   >
   >デフォルトでは、ユーザーが作成したスキーマは「cus」名前空間に保存されます。 詳しくは、[スキーマの ID](../../configuration/using/about-schema-reference.md#identification-of-a-schema) を参照してください。

1. テーブルの内容を作成します。 設定が欠落していないことを確認するには、入力ウィザードを使用することをお勧めします。 それには、「**[!UICONTROL 挿入]**」ボタンをクリックし、追加する設定のタイプを選択します。

   ![](assets/s_ncs_configuration_create_new_content.png)

1. 契約テーブルの設定を定義します。

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

   契約のタイプを追加し、契約番号にインデックスを配置します。

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

1. データベース構造を更新して、スキーマのリンク先となるテーブルを作成します。 詳しくは、 [データベース構造の更新](../../configuration/using/updating-the-database-structure.md).
