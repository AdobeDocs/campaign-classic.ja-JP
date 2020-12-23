---
solution: Campaign Classic
product: campaign
title: Adobe Experience Cloud Triggers 用の Adobe I/O の設定
description: Adobe Experience Cloud Triggers 用の Adobe I/O の設定方法を説明します
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 55ca41bfcacbd75846901474ae6f012dfdc8d1a9
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Experience Cloud Triggers 用の Adobe I/O の設定{#configuring-adobe-io}

>[!CAUTION]
>
>oAuth 認証を通じて古いバージョンの Triggers 統合を使用する場合は、**以下の説明に従って Adobe I/O に移行する必要があります**。 従来の oAuth 認証モードは、2021 年 4 月 30 日に廃止されます。[詳細情報](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411)

## 前提条件 {#adobe-io-prerequisites}

この統合は、**Campaign Classic20.3、20.2.4、19.1.8およびGold Standard 11リリース**&#x200B;からのみ適用されます。

この実装を開始する前に、以下の点を確認してください。

* 有効な&#x200B;**組織識別子**:identity managementシステム(IMS)の組織識別子は、Adobe Experience Cloud内の一意の識別子で、VisitorIDサービスやIMSシングルサインオン(SSO)などに使用されます。 [詳細情報](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html)
* 組織への&#x200B;**開発者アクセス**。  [このページ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)で説明する手順に従い、すべての製品プロファイルに関してこのアクセス権を提供するには、IMS 組織のシステム管理者権限をリクエストする必要があります。
>
## 手順 1：Adobe I/O プロジェクトの作成と更新 {#creating-adobe-io-project}

1. Adobe I/Oにアクセスし、IMS組織のシステム管理者権限でログインします。

   >[!NOTE]
   >
   > 正しい組織ポータルにログインしていることを確認します。

1. 既存の統合クライアント ID をインスタンス設定ファイル（ims/authIMSTAClientId）から抽出します。既存の属性または空の属性は、クライアント識別子が設定されていないことを示します。

   >[!NOTE]
   >
   >クライアントIDが空の場合は、直接&#x200B;**[!UICONTROL 新しいプロジェクト]**&#x200B;をAdobe I/Oに作成できます。

1. 抽出したクライアント識別子を使用して、既存のプロジェクトを識別します。 前の手順で抽出したものと同じクライアント識別子を持つ既存のプロジェクトを探します。

   ![](assets/do-not-localize/adobe_io_8.png)

1. 「**[!UICONTROL + Add to Project]**」を選択して、「**[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/adobe_io_1.png)

1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL Adobe Analytics]**」を選択します。

   ![](assets/do-not-localize/adobe_io_2.png)

1. 認証のタイプとして「**[!UICONTROL Service Account (JWT)]**」を選択します。

   ![](assets/do-not-localize/adobe_io_3.png)

1. クライアント ID が空の場合は、「**[!UICONTROL キーペアを生成]**」を選択して、公開鍵と秘密鍵のペアを作成します。

   ![](assets/do-not-localize/adobe_io_4.png)

1. 公開鍵をアップロードし、「**[!UICONTROL Next]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_5.png)

1. 「**Analytics-&lt;組織名>**」という製品プロファイルを選択し、「**[!UICONTROL Save configured API]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_6.png)

1. プロジェクトから、「**[!UICONTROL Service Account (JWT)]**」を選択し、次の情報をコピーします。
   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

   ![](assets/do-not-localize/adobe_io_7.png)

## 手順 2：Adobe Campaign にプロジェクト資格情報を追加 {#add-credentials-campaign}

Adobe Campaign にプロジェクト資格情報を追加するには、Adobe Campaign インスタンスのすべてのコンテナで「neolane」ユーザーとして次のコマンドを実行し、**[!UICONTROL テクニカルアカウント]**&#x200B;資格情報をインスタンス設定ファイルに挿入します。

```
nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID[/Client_Secret[/Base64_encoded_Private_Key]]
```

>[!NOTE]
>
>秘密鍵は base64 UTF-8 形式でエンコードする必要があります。秘密鍵でない場合は、鍵をエンコードする前に、鍵から新しい行を削除してください。秘密鍵は、統合の作成に使用したものと同じである必要があります。

## 手順 3：pipelined タグを更新 {#update-pipelined-tag}

[!DNL pipelined] タグを更新するには、設定ファイル（**config-&lt;インスタンス名>.xml**）で、認証タイプを以下のように Adobe I/O プロジェクトに更新する必要があります。

```
<pipelined ... authType="imsJwtToken"  ... />
```
