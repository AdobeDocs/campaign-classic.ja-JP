---
solution: Campaign Classic
product: campaign
title: シードアドレス
description: シードアドレス
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%

---


# シードアドレス{#seed-addresses}

受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 **[!UICONTROL nms:seedMember]**&#x200B;スキーマを拡張する必要があります。 以下に示すように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使い方の詳細は、[この](../../delivery/using/about-seed-addresses.md)を参照してください。

## 実装 {#implementation}

**nms:seedMember**&#x200B;スキーマと、あらかじめ用意されているリンクされたフォームは、すべての必要なフィールドを参照するように、顧客の設定用に拡張する必要があります。 スキーマ定義には、その設定モードに関するコメントが含まれています。

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

1. **nms:seedMember**&#x200B;スキーマの拡張子を作成します。 詳しくは、[スキーマの拡張](../../configuration/using/extending-a-schema.md)を参照してください。
1. この新しい拡張機能では、次のパラメーターを使用して、**[!UICONTROL seedMember]**&#x200B;のルートに新しい要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   このキャンペーンには、要素の書き出しに必要なフィールドが含まれている必要があります。 これらのフィールドは、外部スキーマの対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが&#x200B;**[!UICONTROL cus:person]**&#x200B;の場合、**[!UICONTROL nms:seedMember]**&#x200B;スキーマは次のように拡張する必要があります。

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
   >**nms:seedMember**&#x200B;スキーマの拡張は、Adobe Campaign内のキャンペーンと配信の構造に従う必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張時に、「email」フィールドに&#x200B;**SQL名(@sqlname)**&#x200B;を指定する必要があります。 SQL名は、受信者スキーマ用に予約されている&#39;sEmail&#39;と異なる必要があります。
   >    * **nms:seedMember**&#x200B;を拡張する際に作成したスキーマを使用して、データベース構造を更新する必要があります。
   >    * **nms:seedMember**&#x200B;拡張子の中で、電子メールアドレスを含むフィールドの属性は&#x200B;**name=&quot;email&quot;**&#x200B;にする必要があります。 SQL名は、受信者スキーマで既に使用されている「sEmail」とは異なる名前にする必要があります。 この属性は&#x200B;**`<element name="custom_cus_person" />`**&#x200B;要素の下で直ちに宣言する必要があります。


1. **[!UICONTROL seedMember]**&#x200B;のフォームを変更し、それに応じて&#x200B;**[!UICONTROL シードアドレス]**&#x200B;ウィンドウの新しい「内部受信者」タブを定義します。 詳しくは、[フォーム構造](../../configuration/using/form-structure.md)を参照してください。

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
