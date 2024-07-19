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
ht-degree: 3%

---

# インターフェイスの設定{#configuring-the-interface}

Adobe Campaign インターフェイスに新しい受信者テーブルを表示してダイアログを表示するには、次の手順に従います。

* 新しい受信者テーブルのコンテンツを編集する新しいフォームを作成します。
* エクスプローラーツリーのフォルダーに新しいタイプを入力します。
* Adobe Campaign ホームページからカスタムテーブルにアクセスする新しい web アプリケーションを作成します。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース（nms:recipient）とのダイアログを行います。 したがって、この変数は変更する必要があります。

1. エクスプローラーの **[!UICONTROL 管理/プラットフォーム/オプション]** ノードに移動します。
1. **Nms_DefaultRcpSchema** 変数の値を、外部受信者テーブルに一致するスキーマの名前に変更します（この場合は cus:individual）。
1. 変更を保存します。

## 新しいフォームの作成 {#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示して編集できるようになります。

>[!IMPORTANT]
>
>フォームの名前は、関係するスキーマの名前と同じである必要があります。

1. エクスプローラーの **管理/設定/入力フォーム** ノードに移動します。
1. **xtk:form** タイプの **form** ファイルを新規作成します。
1. テーブルテンプレートに応じて、必要なすべての監視フィールドとフィールドについて説明します。

   >[!NOTE]
   >
   >**form** タイプのファイルについて詳しくは、[ このページ ](../../configuration/using/identifying-a-form.md) を参照してください。

   この現在の例では、**form** ファイルは **cus:individual** スキーマに基づく必要があるため、次のレイアウトになります。

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

1. **[!UICONTROL 管理/設定/ナビゲーション階層]** ノードに移動します。
1. 新しい **xtk:navtree** タイプ **navtree** ドキュメントを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視フィールドとフィールドについて説明します。

   >[!NOTE]
   >
   >**navtree** タイプのファイルについて詳しくは、[ このページ ](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy) を参照してください。

   現在の例では、**navtree** ファイルは **cus:individual** スキーマに基づく必要があるため、次の形式にします。

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
