---
solution: Campaign Classic
product: campaign
title: インターフェイスの設定
description: インターフェイスの設定
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 3%

---


# インターフェイスの設定{#configuring-the-interface}

Adobe Campaignインターフェイスの新しい受信者テーブルで表示とダイアログを行うには、次の手順を適用します。

* 新しい受信者テーブルの内容を編集するための新しいフォームを作成します。
* エクスプローラツリーのフォルダに新しいタイプを入力します。
* Adobe Campaignホームページを使用してカスタムテーブルにアクセスする新しいWebアプリケーションを作成します。

Adobe Campaignは、「Nms_DefaultRcpSchema」グローバル変数を使用して、デフォルトの受信者受信者(nms:database)との対話を行います。 したがって、この変数は変更する必要があります。

1. エクスプローラーの&#x200B;**[!UICONTROL 管理>プラットフォーム>オプション]**&#x200B;ノードに移動します。
1. **Nms_DefaultRcpSchema**&#x200B;変数の値を、外部受信者テーブル（この場合は次のように）と一致するスキーマの名前に変更します。cus:indival)。
1. 変更を保存します。

## 新しいフォームの作成{#creating-a-new-form-}

新しいフォームを作成すると、外部受信者テーブルのデータを表示および編集できます。

>[!IMPORTANT]
>
>フォームの名前は、対象となるスキーマの名前と同じにする必要があります。

1. エクスプローラーの&#x200B;**管理/設定/入力フォーム**&#x200B;ノードに移動します。
1. 新しい&#x200B;**xtk:form**&#x200B;タイプ&#x200B;**form**&#x200B;ファイルを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >**form**&#x200B;型のファイルの詳細については、[このページ](../../configuration/using/identifying-a-form.md)を参照してください。

   この例では、**フォーム**&#x200B;ファイルは&#x200B;**cus:individual**&#x200B;スキーマに基づいている必要があり、次のレイアウトを持つ必要があります。

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

## ナビゲーション階層{#creating-a-new-type-of-folder-in-the-navigation-hierarchy}に新しいタイプのフォルダーを作成する

1. **[!UICONTROL [管理]>[設定]>[ナビゲーション階層]]**&#x200B;ノードに移動します。
1. 新しい&#x200B;**xtk:navtree**&#x200B;タイプ&#x200B;**navtree**&#x200B;ドキュメントを作成します。
1. テーブルテンプレートに応じて、必要なすべての監視とフィールドについて説明します。

   >[!NOTE]
   >
   >**navtree**&#x200B;タイプのファイルについて詳しくは、[このページ](../../configuration/using/about-navigation-hierarchy.md)を参照してください。

   現在の例では、**navtree**&#x200B;ファイルは&#x200B;**cus:individual**&#x200B;スキーマに基づいている必要があり、次の形式になっています。

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

