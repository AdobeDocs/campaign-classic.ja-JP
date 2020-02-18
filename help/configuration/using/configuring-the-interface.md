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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# インターフェイスの設定{#configuring-the-interface}

Adobe Campaignインターフェイスで新しい受信者テーブルを表示し、ダイアログを表示するには、次の手順を適用します。

* 新しい受信者テーブルのコンテンツを編集するための新しいフォームを作成します。
* エクスプローラツリーのフォルダに新しいタイプを入力します。
* Adobe Campaignホームページからカスタムテーブルにアクセスする新しいWebアプリケーションを作成します。

Adobe Campaignでは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース(nms:recipient)との対話を行います。 したがって、この変数は変更する必要があります。

1. エクスプローラ **[!UICONTROL Administration>Platform>Options]** ーのノードに移動します。
1. Nms_DefaultRcpSchema変数の値を **** 、外部の受信者テーブルに一致するスキーマの名前に変更します(この場合は、次のように指定します。cus:individual)。
1. 変更を保存します。

## Creating a new form {#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示および編集できます。

>[!IMPORTANT]
>
>フォームの名前は、対象となるスキーマの名前と同じにする必要があります。

1. エクスプローラ **ーの管理/設定/Input forms** ノードに移動します。
1. 新しい **xtk:form** typeフォームファ **イルを作成** 。
1. テーブルテンプレートに応じて必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >フォームタイプファイルの詳 **細は** 、このページを参照し [てください](../../configuration/using/identifying-a-form.md)。

   現在の例では、フォームファ **イルは** cus:individualスキーマに基づいている必要があるので **** 、次のレイアウトを持つ必要があります。

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

1. ノードに移動し **[!UICONTROL Administration>Configuration>Navigation hierarchies]** ます。
1. 新しい **xtk:navtreeタイプのnavtree** ドキュメント **を作成します** 。
1. テーブルテンプレートに応じて必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >navtreeタイプのファ **イルの詳細については** 、このページを参照 [してください](../../configuration/using/about-navigation-hierarchy.md)。

   現在の例では、navtreeファイルは **cus:individual** schemaに基づいている必要があるので **** 、次の形式をとっています。

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

