---
product: campaign
title: インターフェイスの設定
description: Campaign インターフェイスの設定方法について説明します
feature: Application Settings
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 9f50f258-845e-4895-b1ef-b73744dea326
TQID: https://experienceleague.adobe.com/KUwDwl9noj6RJa0wn6ZEVnCBRLdOUMoSTf-5b1PrH-g
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 304
ht-degree: 3%

---

# インターフェイスの設定{#configuring-the-interface}

Adobe Campaign インターフェイスで新しい受信者テーブルを表示してダイアログを表示するには、次の手順を実行します。

* 新しい受信者テーブルのコンテンツを編集するための新しいフォームを作成します。
* エクスプローラーツリーのフォルダーに新しいタイプを入力します。
* 新しいweb アプリケーションを作成して、Adobe Campaign ホームページからカスタムテーブルにアクセスします。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース（nms:recipient）と対話します。 したがって、この変数を変更する必要があります。

1. エクスプローラーの&#x200B;**[!UICONTROL 管理> プラットフォーム > オプション]** ノードに移動します。
1. **Nms_DefaultRcpSchema**&#x200B;変数の値を、外部受信者テーブルに一致するスキーマの名前（この場合はcus:individual）に変更します。
1. 変更を保存します。

## 新しいフォームの作成 {#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示および編集できるようになります。

>[!IMPORTANT]
>
>フォームの名前は、関係するスキーマの名前と同じである必要があります。

1. エクスプローラーの&#x200B;**管理/設定/入力フォーム** ノードに移動します。
1. 新しい&#x200B;**xtk:form** タイプ **form** ファイルを作成します。
1. テーブルテンプレートに応じて、必要なモニタリングとフィールドをすべて記述します。

   >[!NOTE]
   >
   >**form**&#x200B;形式のファイルについて詳しくは、[このページ &#x200B;](../../configuration/using/identifying-a-form.md)を参照してください。

   現在の例では、**form** ファイルは&#x200B;**cus:individual** スキーマに基づいている必要があり、したがって次のレイアウトを持っている必要があります。

   ```
   <container colspan="2">
       <input xpath="@id"/>
       <static type="separator"/>
   </container>
   <container colcount="2">
       <input xpath="@lastName"/>
       <input xpath="@firstName"/>
       <input xpath="@email"/>
       <input xpath="@mobile"/>
   </container> 
   ```

1. 作成を保存します。

## ナビゲーション階層に新しいタイプのフォルダーを作成する {#creating-a-new-type-of-folder-in-the-navigation-hierarchy}

1. **[!UICONTROL 管理/設定/ナビゲーション階層]** ノードに移動します。
1. 新しい&#x200B;**xtk:navtree** タイプ **navtree** ドキュメントを作成します。
1. テーブルテンプレートに応じて、必要なモニタリングとフィールドをすべて記述します。

   現在の例では、**navtree** ファイルは&#x200B;**cus:individual** スキーマに基づいている必要があるため、次の形式になります。

   ```
    <model name="root">
       <nodeModel img="nms:usergrp.png" label="My recipient table" name="cusindividual">
         <view name="listdet" schema="cus:individual" type="listdet">
           <columns>
             <node xpath="@id"/>
             <node xpath="@lastName"/>
             <node xpath="@firstName"/>
             <node xpath="@email"/>
             <node xpath="@mobile"/>
           </columns>
         </view>
       </nodeModel>
   </model>
   ```

1. 作成を保存します。
