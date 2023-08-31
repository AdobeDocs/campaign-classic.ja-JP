---
product: campaign
title: インターフェイスの設定
description: Campaign インターフェイスの設定方法を説明します。
feature: Application Settings
role: Data Engineer, Developer
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 9f50f258-845e-4895-b1ef-b73744dea326
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---

# インターフェイスの設定{#configuring-the-interface}

Adobe Campaignインターフェイスで新しい受信者テーブルを表示し、ダイアログを表示するには、次の手順に従います。

* 新しいフォームを作成して、新しい受信者テーブルのコンテンツを編集します。
* エクスプローラーツリーのフォルダーに新しいタイプを入力します。
* 新しい Web アプリケーションを作成し、Adobe Campaignホームページからカスタムテーブルにアクセスします。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース (nms:recipient) とのダイアログを作成します。 したがって、この変数は変更する必要があります。

1. 次に移動： **[!UICONTROL 管理/プラットフォーム/オプション]** エクスプローラーのノード。
1. 値を **Nms_DefaultRcpSchema** 変数に含まれます。この変数は、外部の受信者テーブルに一致するスキーマの名前です（この場合は cus:individual）。
1. 変更を保存します。

## 新しいフォームの作成 {#creating-a-new-form-}

新しいフォームを作成すると、外部の受信者テーブルのデータを表示および編集できます。

>[!IMPORTANT]
>
>フォームの名前は、対象となるスキーマの名前と同じにする必要があります。

1. 次に移動： **管理/設定/入力フォーム** エクスプローラーのノード。
1. 新規作成 **xtk:form** type **フォーム** ファイル。
1. テーブルテンプレートに応じて、必要なすべての監視およびフィールドについて説明します。

   >[!NOTE]
   >
   >詳しくは、 **フォーム** タイプファイル： [このページ](../../configuration/using/identifying-a-form.md).

   現在の例では、 **フォーム** ファイルは、 **cus:individual** スキーマを作成し、次のレイアウトにする必要があります。

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

1. 次に移動： **[!UICONTROL [ 管理 ] > [ 設定 ] > [ ナビゲーション階層 ]]** ノード。
1. 新規作成 **xtk:navtree** type **ナブツリー** 文書。
1. テーブルテンプレートに応じて、必要なすべての監視およびフィールドについて説明します。

   >[!NOTE]
   >
   >詳しくは、 **ナブツリー** タイプファイル： [このページ](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy).

   現在の例では、 **ナブツリー** ファイルは、 **cus:individual** スキーマを作成し、次の形式を取ります。

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
