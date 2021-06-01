---
product: campaign
title: シードアドレス
description: シードアドレス
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: a16103bf-0498-4f59-ad96-8bfdeea26577
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%

---

# シードアドレス{#seed-addresses}

受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 **[!UICONTROL nms:seedMember]**&#x200B;スキーマを拡張する必要があります。 次に示すように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、[この節](../../delivery/using/about-seed-addresses.md)を参照してください。

## 実装 {#implementation}

**nms:seedMember**&#x200B;スキーマと、すぐに使用できるリンクされたフォームは、必要なすべてのフィールドを参照するように、顧客の設定用に拡張する必要があります。 スキーマ定義には、その設定モードの詳細を示すコメントが含まれます。

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

1. **nms:seedMember**&#x200B;スキーマの拡張を作成します。 詳しくは、[スキーマの拡張](../../configuration/using/extending-a-schema.md)を参照してください。
1. この新しい拡張機能では、次のパラメーターを使用して、**[!UICONTROL seedMember]**&#x200B;のルートに新しい要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、キャンペーンのエクスポートに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマ内の対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが&#x200B;**[!UICONTROL cus:person]**&#x200B;の場合、 **[!UICONTROL nms:seedMember]**&#x200B;スキーマは次のように拡張する必要があります。

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
   >**nms:seedMember**&#x200B;スキーマの拡張は、Adobe Campaignのキャンペーンと配信の構造に準拠する必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張の際に、「email」フィールドに&#x200B;**SQL名(@sqlname)**&#x200B;を指定する必要があります。 SQL名は、受信者スキーマ用に予約されている「sEmail」とは異なる名前にする必要があります。
   >    * **nms:seedMember**&#x200B;を拡張する際に作成したスキーマでデータベース構造を更新する必要があります。
   >    * **nms:seedMember**&#x200B;拡張機能では、電子メールアドレスを含むフィールドの属性を&#x200B;**name=&quot;email&quot;**&#x200B;にする必要があります。 SQL名は、受信者スキーマに既に使用されている「sEmail」とは異なる名前にする必要があります。 この属性は、**`<element name="custom_cus_person" />`**&#x200B;要素の下で直ちに宣言する必要があります。


1. **[!UICONTROL seedMember]**&#x200B;フォームを変更し、**[!UICONTROL シードアドレス]**&#x200B;ウィンドウで新しい「内部受信者」タブを定義します。 詳しくは、[フォーム構造](../../configuration/using/form-structure.md)を参照してください。

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

シードアドレスの属性がすべて入力されていない場合、Adobe Campaignは自動的に次のプロファイルを置き換えます。既存のプロファイルのデータを使用して、パーソナライゼーションの際に自動的に入力されます。
