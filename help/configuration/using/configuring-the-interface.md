---
product: campaign
title: インターフェイスの設定
description: インターフェイスの設定
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 9f50f258-845e-4895-b1ef-b73744dea326
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 3%

---

# インターフェイスの設定{#configuring-the-interface}

![](../../assets/v7-only.svg)

Adobe Campaignインターフェイスで新しい受信者テーブルを表示してダイアログを表示するには、次の手順に従います。

* 新しいフォームを作成して、新しい受信者テーブルの内容を編集します。
* エクスプローラーツリーのフォルダーに新しいタイプを入力します。
* 新しい Web アプリケーションを作成し、Adobe Campaignホームページからカスタムテーブルにアクセスします。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者データベース (nms:recipient) と対話します。 この変数は変更する必要があります。

1. エクスプローラーの **[!UICONTROL 管理/プラットフォーム/オプション]** ノードに移動します。
1. **Nms_DefaultRcpSchema** 変数の値を、外部の受信者テーブル ( この場合はcus:individual)。
1. 変更を保存します。

## 新しいフォームの作成 {#creating-a-new-form-}

新しいフォームを作成すると、外部の受信者テーブルのデータを表示および編集できます。

>[!IMPORTANT]
>
>フォームの名前は、対象となるスキーマの名前と同じにする必要があります。

1. エクスプローラーの **管理/設定/入力フォーム** ノードに移動します。
1. 新しい **xtk:form** タイプ **form** ファイルを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視およびフィールドについて説明します。

   >[!NOTE]
   >
   >**form** タイプのファイルの詳細については、[ このページ ](../../configuration/using/identifying-a-form.md) を参照してください。

   この例では、**form** ファイルは **cus:individual** スキーマに基づいている必要があるので、次のレイアウトにする必要があります。

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
1. テーブルテンプレートに応じて、必要なすべての監視およびフィールドについて説明します。

   >[!NOTE]
   >
   >**navtree** タイプのファイルについて詳しくは、[ このページ ](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy) を参照してください。

   現在の例では、**navtree** ファイルは **cus:individual** スキーマに基づいている必要があるので、次の形式にする必要があります。

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
