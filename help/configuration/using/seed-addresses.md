---
product: campaign
title: シードアドレス
description: シードアドレス
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
feature: Seed Address
exl-id: a16103bf-0498-4f59-ad96-8bfdeea26577
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 8%

---

# シードアドレス{#seed-addresses}



受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 この **[!UICONTROL nms:seedMember]** スキーマを拡張する必要があります。 次に示すように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、 [この節](../../delivery/using/about-seed-addresses.md).

## 実装 {#implementation}

この **nms:seedMember** すべての必要なフィールドを参照するよう、スキーマとリンクされたフォーム（標準搭載）を顧客の設定用に拡張することを目的としています。 スキーマ定義には、その設定モードを説明するコメントが含まれています。

受信者テーブルの拡張スキーマの定義：

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

1. の拡張機能の作成 **nms:seedMember** スキーマ。 詳しくは、[この節](../../configuration/using/extending-a-schema.md)を参照してください。
1. この新しい拡張機能で、のルートに新しい要素を追加します。 **[!UICONTROL seedMember]** を次のパラメーターと共に使用します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、キャンペーンのエクスポートに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマ内の対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが **[!UICONTROL cus:person]** 、 **[!UICONTROL nms:seedMember]** スキーマは、次のように拡張する必要があります。

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
   >の拡張 **nms:seedMember** スキーマは、Adobe Campaignでのキャンペーンと配信の構造に従う必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張機能の間、 **SQL 名 (@sqlname)** （「email」フィールド）に入力します。 SQL 名は、受信者スキーマ用に予約されている「sEmail」とは異なる名前にする必要があります。
   >    * データベース構造を、の拡張時に作成したスキーマで更新する必要があります **nms:seedMember**.
   >    * 内 **nms:seedMember** 拡張子の場合、E メールアドレスを格納するフィールドには、 **name=&quot;email&quot;** 属性として。 SQL 名は、受信者スキーマに既に使用されている「sEmail」とは異なる名前を使用する必要があります。 この属性は、 **`<element name="custom_cus_person" />`** 要素。
   >    
   >

1. を変更します。 **[!UICONTROL seedMember]** それに応じてフォームを作成し、 **[!UICONTROL シードアドレス]** ウィンドウ 詳しくは、[このページ](../../configuration/using/form-structure.md)を参照してください。

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

シードアドレスのすべての属性が入力されていない場合、Adobe Campaignは次のプロファイルを自動的に置き換えます。既存のプロファイルのデータを使用したパーソナライゼーション時に、自動的に入力されます。
