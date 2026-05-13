---
product: campaign
title: シードアドレス
description: シードアドレス
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Seed Address
level: Intermediate, Experienced
exl-id: a16103bf-0498-4f59-ad96-8bfdeea26577
TQID: https://experienceleague.adobe.com/xEP-TmMNJ0On70jE2PdjywSXeXw5oF0LVeCDiA7nKB8
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 10%

---

# シードアドレス{#seed-addresses}



受信者テーブルがカスタムテーブルの場合は、追加の設定が必要です。 **[!UICONTROL nms:seedMember]** スキーマを拡張する必要があります。 以下に示すように、適切なフィールドを定義するための追加のタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

シードアドレスの使用について詳しくは、[この節](../../delivery/using/about-seed-addresses.md)を参照してください。

## 実装 {#implementation}

**nms:seedMember** スキーマとリンクされたフォームは、すべての必要なフィールドを参照するために、顧客設定のために拡張することを目的としています。 スキーマ定義には、設定モードの詳細を説明するコメントが含まれています。

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

1. **nms:seedMember** スキーマの拡張機能を作成します。 詳しくは、[この節](../../configuration/using/extending-a-schema.md)を参照してください。
1. この新しい拡張機能では、次のパラメーターを使用して、**[!UICONTROL seedMember]**&#x200B;のルートに新しい要素を追加します。

   ```
   name="custom_customNamespace_customSchema"
   ```

   この要素には、キャンペーンの書き出しに必要なフィールドを含める必要があります。 これらのフィールドは、外部スキーマの対応するフィールドと同じ名前にする必要があります。 例えば、スキーマが&#x200B;**[!UICONTROL cus:person]**&#x200B;の場合、**[!UICONTROL nms:seedMember]** スキーマは次のように拡張する必要があります。

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
   >**nms:seedMember** スキーマの拡張機能は、Adobe Campaignでのキャンペーンと配信の構造に準拠している必要があります。

   >[!IMPORTANT]
   >
   >
   >    
   >    
   >    * 拡張機能では、「メール」フィールドに&#x200B;**SQL名（@sqlname）**&#x200B;を指定する必要があります。 SQL名は、受信者スキーマ用に予約されている「sEmail」とは異なる必要があります。
   >    * **nms:seedMember**&#x200B;の拡張時に作成されたスキーマで、データベース構造を更新する必要があります。
   >    * **nms:seedMember**&#x200B;拡張機能では、電子メールアドレスを含むフィールドに属性として&#x200B;**name=&quot;email&quot;**&#x200B;が必要です。 SQL名は、受信者スキーマに既に使用されている「sEmail」とは異なる必要があります。 この属性は、**`<element name="custom_cus_person" />`**&#x200B;要素の下ですぐに宣言する必要があります。
   >    
   >

1. **[!UICONTROL seedMember]** フォームを変更して、**[!UICONTROL シードアドレス]** ウィンドウで新しい「内部受信者」タブを定義します。 詳しくは、[このページ](../../configuration/using/form-structure.md)を参照してください。

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

シードアドレスのすべての属性が入力されていない場合、Adobe Campaignはプロファイルを自動的に置き換えます。プロファイルは、既存のプロファイルのデータを使用してパーソナライゼーション中に自動的に入力されます。
