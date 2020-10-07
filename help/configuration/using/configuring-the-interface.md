---
title: インターフェイスの設定
seo-title: インターフェイスの設定
description: インターフェイスの設定
seo-description: null
page-status-flag: never-activated
uuid: 101ba02f-da43-4dcc-b9ff-6e5ca848fc5d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: 8fb9ff23-17a7-4425-9195-738d6fd914dc
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 4%

---


# インターフェイスの設定{#configuring-the-interface}

Adobe Campaignインターフェイスの新しい受信者テーブルで表示とダイアログを行うには、次の手順を適用します。

* 新しい受信者テーブルの内容を編集するための新しいフォームを作成します。
* エクスプローラツリーのフォルダに新しいタイプを入力します。
* Adobe Campaignホームページを使用してカスタムテーブルにアクセスする新しいWebアプリケーションを作成します。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者受信者(nms:database)との対話を行います。 したがって、この変数は変更する必要があります。

1. エクスプローラーの **[!UICONTROL 管理/プラットフォーム/オプション]** ・ノードに移動します。
1. Nms_DefaultRcpSchema **** 変数の値を、外部受信者テーブル（この場合は次のように指定）と一致するスキーマの名前に変更します。cus:indival)。
1. 変更を保存します。

## Creating a new form {#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示および編集できます。

>[!IMPORTANT]
>
>フォームの名前は、対象となるスキーマの名前と同じにする必要があります。

1. エクスプローラーの **管理/設定/Input forms** ノードに移動します。
1. 新しい **xtk:form** type **form** fileを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >フ **ォームタイプファイルの詳細については、** このページを参照してください [](../../configuration/using/identifying-a-form.md)。

   この例では、 **フォームファイルが** cus:individual **** スキーマに基づいている必要があるので、次のレイアウトを使用します。

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

1. [ **[!UICONTROL 管理] > [設定] > [ナビゲーション階層]** ]ノードに移動します。
1. 新しい **xtk:navtree** タイプのnavtree **** ドキュメントを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >navtree **タイプのファイルについて詳しくは、** このページを参照してください [](../../configuration/using/about-navigation-hierarchy.md)。

   この例では、navtree **ファイルは** cus:individual **** スキーマに基づいている必要があるので、次の形式を持ちます。

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

