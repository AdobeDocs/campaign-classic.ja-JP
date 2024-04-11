---
product: campaign
title: インターフェイスの設定
description: Campaign インターフェイスの設定方法を学ぶ
feature: Application Settings
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 9f50f258-845e-4895-b1ef-b73744dea326
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---

# インターフェイスの設定{#configuring-the-interface}

Adobe Campaign インターフェイスに新しい受信者テーブルを表示してダイアログを表示するには、次の手順に従います。

* 新しい受信者テーブルのコンテンツを編集する新しいフォームを作成します。
* エクスプローラーツリーのフォルダーに新しいタイプを入力します。
* Adobe Campaign ホームページからカスタムテーブルにアクセスする新しい web アプリケーションを作成します。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース（nms:recipient）とのダイアログを行います。 したがって、この変数は変更する必要があります。

1. に移動します **[!UICONTROL 管理/プラットフォーム/オプション]** エクスプローラーのノード。
1. の値を **Nms_DefaultRcpSchema** 外部受信者テーブルに一致するスキーマの名前を持つ変数（この場合は cus:individual）。
1. 変更を保存します。

## 新しいフォームの作成 {#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示して編集できるようになります。

>[!IMPORTANT]
>
>フォームの名前は、関係するスキーマの名前と同じである必要があります。

1. に移動します **管理/設定/入力フォーム** エクスプローラーのノード。
1. 新しいを作成 **xtk:form** タイプ **フォーム** ファイル。
1. テーブルテンプレートに応じて、必要なすべての監視フィールドとフィールドについて説明します。

   >[!NOTE]
   >
   >詳しくは、 **フォーム** ファイルを入力します。を参照してください [このページ](../../configuration/using/identifying-a-form.md).

   現在の例では、 **フォーム** ファイルはに基づいている必要があります **cus:individual** スキーマなので、次のレイアウトになります。

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

## ナビゲーション階層での新しいタイプのフォルダーの作成 {#creating-a-new-type-of-folder-in-the-navigation-hierarchy}

1. に移動します **[!UICONTROL 管理/設定/ナビゲーション階層]** ノード。
1. 新しいを作成 **xtk:navtree** タイプ **navtree** ドキュメント。
1. テーブルテンプレートに応じて、必要なすべての監視フィールドとフィールドについて説明します。

   >[!NOTE]
   >
   >詳しくは、 **navtree** ファイルを入力します。を参照してください [このページ](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy).

   現在の例では、 **navtree** ファイルはに基づいている必要があります **cus:individual** スキーマなので、次の形式になります。

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
