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
source-git-commit: d5c1732858fd5d079bbd9a755997c04adf5c9d47

---


# シードアドレス{#seed-addresses}

受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 The **[!UICONTROL nms:seedMember]** schema must be extended. 以下に示すように、適切なフィールドを定義するシードアドレスにタブが追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用方法の詳細は、この節を参 [照してくださ](../../delivery/using/about-seed-addresses.md)い。

## 実装 {#implementation}

nms:seedMember **** スキーマと、あらかじめ用意されているリンクされたフォームは、すべての必要なフィールドを参照するように、顧客設定用に拡張されます。 スキーマ定義には、設定モードの詳細を示すコメントが含まれます。

拡張受信者の定義：

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

1. nms:seedMember拡張を作 **成します** 。 詳しくは、「拡張機能」を参照 [してください](../../configuration/using/extending-a-schema.md)。
1. この新しい拡張機能で、次のパラメーターを使用して、のルートに新しい **[!UICONTROL seedMember]** 要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、要素の書き出しに必要なフィールドを含める必要があります。キャンペーン これらのフィールドは、外部フィールド内の対応するフィールドと同じ名前を持つ必要があります。スキーマ 例えば、スキーマがの場合、 **[!UICONTROL cus:person]** スキーマは次のよ **[!UICONTROL nms:seedMember]** うに拡張されます。

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
   >nms:seedMember **スキーマの拡張は** 、キャンペーンと配信の構造に準拠する必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張時に、「email」フィールドに **SQL名(@sqlname)を指定する必要があります** 。 SQL名は、受信者スキーマ用に予約されている「sEmail」と異なる必要があります。
   >    * nms:seedMemberを拡張する際に作成したスキーマでデータベース構造を更新する **必要があります**。
   >    * nms:seedMember **拡張では、電子メールアドレスを含むフィールド** の属性はname=&quot;email&quot;である必要があります **** 。 SQL名は、既に受信者スキーマに使用されている「sEmail」とは異なる名前にする必要があります。 この属性は、要素の下で直ちに宣言する必要があ **`<element name="custom_cus_person" />`** ります。


1. それに応じてフ **[!UICONTROL seedMember]** ォームを変更し、ウィンドウに新しい「内部受信者」タブを定義 **[!UICONTROL Seed addresses]** します。 For more on this, refer to [Form structure](../../configuration/using/form-structure.md).

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

シードアドレスのすべての属性が入力されない場合、Adobe Campaignは自動的に次のプロファイルを置き換えます。既存のデータを使用したパーソナライゼーション時に、自動的に入力されます。プロファイル
