---
product: campaign
title: シードアドレス
description: シードアドレス
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Seed Address
exl-id: a16103bf-0498-4f59-ad96-8bfdeea26577
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 10%

---

# シードアドレス{#seed-addresses}



受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 **[!UICONTROL nms:seedMember]** スキーマを拡張する必要があります。 次に示すように、適切なフィールドを定義するためのシードアドレスにタブが追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、[ この節 ](../../delivery/using/about-seed-addresses.md) を参照してください。

## 実装 {#implementation}

**nms:seedMember** スキーマと、すぐに使用できるリンクフォームは、顧客の設定用に拡張して、必要なすべてのフィールドを参照することを目的としています。 スキーマ定義には、設定モードを説明するコメントが含まれています。

受信者テーブル拡張スキーマの定義：

```
<srcSchema label="Person" name="person" namespace="cus">
  <element autopk="true" label="Person" name="person">
      <attribute label="LastName" name="lastname" type="string"/>
      <attribute label="FirstName" name="firstname" type="string"/>
    <element label="Address" name="address">
      <attribute label="Email" name="addrEnv" type="string"/>
    </element>
    <attribute label="Code Offer" name="codeOffer" type="string"/>
  </element>
</srcSchema>
```

次の手順に従います。

1. **nms:seedMember** スキーマの拡張を作成します。 詳しくは、[この節](../../configuration/using/extending-a-schema.md)を参照してください。
1. この新しい拡張機能では、**[!UICONTROL seedMember]** のルートに、次のパラメーターで新しい要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、キャンペーンのエクスポートに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマの対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが **[!UICONTROL cus:person]** の場合、**[!UICONTROL nms:seedMember]** スキーマは次のように拡張する必要があります。

   ```
     <srcSchema extendedSchema="nms:seedMember" label="Seed addresses" labelSingular="Seed address" name="seedMember" namespace="cus">
     <element name="common">
       <element name="custom_cus_person">
         <attribute name="lastname" template="cus:person:person/@lastname"/>
         <attribute name="firstname" template="cus:person:person/@firstname"/>
         <attribute name="email" sqlname="myEmailField" template="cus:person:person/address/@addrEnv" xml="false"/>
       </element>
     </element>
     <element name="seedMember">
      <element aggregate="cus:seedMember:common"/>
     </element>
   </srcSchema>
   ```

   >[!NOTE]
   >
   >**nms:seedMember** スキーマの拡張は、Adobe Campaignのキャンペーンと配信の構造に従う必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張時に、「電子メール」フィールドに **SQL 名（@sqlname）** を指定する必要があります。 SQL 名は、受信者スキーマ用に予約されている「sEmail」とは異なる必要があります。
   >    * **nms:seedMember** を拡張するときに作成したスキーマでデータベース構造を更新する必要があります。
   >    * **nms:seedMember** 拡張機能では、メールアドレスを含むフィールドの属性として **name=&quot;email&quot;** が必要です。 SQL 名は、受信者スキーマに既に使用されている「sEmail」とは異なる名前にする必要があります。 この属性は、**`<element name="custom_cus_person" />`** 要素の下で直ちに宣言する必要があります。
   >    
   >

1. **[!UICONTROL seedMember]** フォームを適宜変更して、「**[!UICONTROL シードアドレス]**」ウィンドウに新しい「内部受信者」タブを定義します。 詳しくは、[このページ](../../configuration/using/form-structure.md)を参照してください。

   ```
   <container colcount="2" label="Internal recipient" name="internal"
                xpath="custom_cus_person">
       <input colspan="2" editable="true" nolabel="true" type="treeEdit">
         <container label="Recipient (cus:person)">
           <input xpath="@last name"/>
           <input xpath="@first name"/>
           <input xpath="@email"/>
         </container>
       </input>
     </container>
   ```

シードアドレスのすべての属性が入力されない場合、Adobe Campaignはプロファイルを自動的に置き換えます。これらは、既存のプロファイルのデータを使用してパーソナライズする際に、自動的に入力されます。
