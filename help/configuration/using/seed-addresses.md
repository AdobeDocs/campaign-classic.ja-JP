---
title: シードアドレス
seo-title: シードアドレス
description: シードアドレス
seo-description: null
page-status-flag: never-activated
uuid: 0ebdeb73-be67-4c34-9f59-9fd4fb5241ab
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: 41338d32-b95c-45ae-bee6-17b2af5bd837
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 912507f25c5bc3c1ca7121b0df8182176900f4c0

---


# シードアドレス{#seed-addresses}

受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 The **[!UICONTROL nms:seedMember]** schema must be extended. 以下に示すように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、この節を参 [照してください](../../delivery/using/about-seed-addresses.md)。

## 実装 {#implementation}

すぐに使 **用できる** nms:seedMemberスキーマとリンクされたフォームは、すべての必要なフィールドを参照するように、顧客設定用に拡張するものです。 スキーマ定義には、その設定モードの詳細を示すコメントが含まれています。

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

1. nms:seedMemberスキーマの拡張 **を作成します** 。 For more on this, refer to [Extending a schema](../../configuration/using/extending-a-schema.md).
1. この新しい拡張機能で、次のパラメーターを使用して、のルートに新しい **[!UICONTROL seedMember]** 要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、キャンペーンのエクスポートに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマ内の対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが次の場合、ス **[!UICONTROL cus:person]** キーマは **[!UICONTROL nms:seedMember]** 次のように拡張されます。

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
   >nms:seedMemberスキーマの拡張は **** 、Adobe Campaignのキャンペーンと配信の構造に準拠している必要があります。

   >[!CAUTION]
   >
   >
   >    
   >    
   >    * 拡張時に、「email」フィールドに **SQL名(@sqlname)を指定する必要があります** 。 SQL名は、受信者のスキーマ用に予約されている「sEmail」と異なる必要があります。
   >    * データベース構造は、 **nms:seedMemberを拡張する際に作成したスキーマで更新する必要があります**。
   >    * nms:seedMember **拡張では** 、電子メールアドレスを含むフィールドの属性 **はname=&quot;email&quot;である必要があります** 。 SQL名は、受信者のスキーマに既に使用されている「sEmail」とは異なる名前にする必要があります。 この属性は、要素の下で直ちに宣言する必要があ **`<element name="custom_cus_person" />`** ります。


1. それに従って **[!UICONTROL seedMember]** フォームを変更し、ウィンドウに新しい「内部受信者」タブを定義 **[!UICONTROL Seed addresses]** します。 For more on this, refer to [Form structure](../../configuration/using/form-structure.md).

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

シードアドレスの属性をすべて入力しない場合、Adobe Campaignは自動的に次のプロファイルを置き換えます。既存のプロファイルのデータを使用したパーソナライゼーション時に自動的に入力されます。
