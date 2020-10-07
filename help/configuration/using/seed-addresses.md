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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# シードアドレス{#seed-addresses}

受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 The **[!UICONTROL nms:seedMember]** schema must be extended. 以下に示すように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、 [この節を参照してください](../../delivery/using/about-seed-addresses.md)。

## 実装 {#implementation}

nms:seedMember **** スキーマとあらかじめ用意されているリンクされたフォームは、お客様の設定用に拡張し、必要なすべてのフィールドを参照するようにします。 スキーマ定義には、その設定モードに関するコメントが含まれています。

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

1. nms:seedMember **** スキーマの拡張子を作成します。 詳しくは、「スキーマの [拡張」を参照してください](../../configuration/using/extending-a-schema.md)。
1. この新しい拡張機能では、次のパラメーターを使用して、 **[!UICONTROL seedMember]** のルートに新しい要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   このキャンペーンには、要素の書き出しに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマの対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが **[!UICONTROL cus:person]** の場合、 **[!UICONTROL nms:seedMember]** スキーマは次のように拡張する必要があります。

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
   >nms:seedMember **** スキーマの拡張は、Adobe Campaign内のキャンペーンと配信の構造に準拠する必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張時に、「email」フィールドに **SQL名(@sqlname)** を指定する必要があります。 SQL名は、受信者スキーマ用に予約されている&#39;sEmail&#39;と異なる必要があります。
   >    * nms:seedMemberを拡張する際に作成したスキーマを使用して、データベース構造を更新する必要があり **ます**。
   >    * nms:seedMember **拡張では、電子メールアドレスを含むフィールドの** 属性は **name=&quot;email&quot;** にする必要があります。 SQL名は、受信者スキーマで既に使用されている「sEmail」とは異なる名前にする必要があります。 この属性は、要素の下で直ちに宣言する必要があり **`<element name="custom_cus_person" />`** ます。


1. 「 **[!UICONTROL seedMember]** 」フォームを適宜変更し、「 **[!UICONTROL シードアドレス]** 」ウィンドウで新しい「内部受信者」タブを定義します。 For more on this, refer to [Form structure](../../configuration/using/form-structure.md).

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

シードアドレスの属性をすべて入力しない場合、Adobe Campaignは自動的にプロファイルを置き換えます。既存のプロファイルのデータを使用したパーソナライゼーション時に、自動的に入力されます。
