---
title: Adobe Experience Cloud・トリガー用のAdobeI/Oの構成
description: Adobe Experience Cloud・トリガー用のAdobeI/Oの構成方法
page-status-flag: never-activated
uuid: e2db7bdb-8630-497c-aacf-242734cc0a72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 1c20795d-748c-4f5d-b526-579b36666e8f
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 160af30e13bb6a81672477f4f801dbd5cc3c767c
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 34%

---


# Configuring Adobe I/O for Adobe Experience Cloud Triggers {#configuring-adobe-io}

>[!CAUTION]
>
>oAuth認証を通じて古いバージョンのTriggers統合を使用する場合は、以下 **の説明に従ってAdobeI/Oに移行する必要があります**。 従来のoAuth認証モードは、2021年4月30日に廃止されます。 [詳細情報](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411)

## 前提条件 {#adobe-io-prerequisites}

この統合は、 **Campaign Classic20.3リリース以降にのみ適用されます**。

この実装を開始する前に、以下の点を確認してください。

* 有効なIMSOrgID:identity managementシステム(IMS)の組織識別子は、Adobe Experience Cloud内の一意の識別子です。この識別子は、VisitorIDサービスやIMSシングルサインオン(SSO)などに使用されます。
* IMS組織への開発者アクセス権。

>[!NOTE]
>
>If you need to request the System Administrator privileges of the IMS Org, follow the procedure detailed [in this page](https://helpx.adobe.com/jp/enterprise/admin-guide.html/jp/enterprise/using/manage-developers.ug.html) to provide this access for the all Product Profiles.


## 手順1:AdobeI/Oプロジェクトの作成/更新 {#creating-adobe-io-project}

1. AdobeI/Oにアクセスし、IMSorgのシステム管理者権限でログインします。

   >[!NOTE]
   >
   > 正しい IMSorg ポータルにログインしていることを確認します。

1. 既存の統合クライアント ID をインスタンス設定ファイル（ims/authIMSTAClientId）から抽出します。既存の属性または空の属性は、クライアントIDが設定されていないことを示します。

   >[!NOTE]
   >
   >If your Client ID is empty, you can directly **[!UICONTROL Create a New project]** in Adobe I/O.

1. 抽出したクライアントIDを使用して、既存のプロジェクトを識別します。 前の手順で抽出されたものと同じクライアント ID を持つ既存のプロジェクトを探します。

   ![](assets/do-not-localize/adobe_io_8.png)

1. 「**[!UICONTROL + Add to Project]**」を選択して、「**[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/adobe_io_1.png)

1. In the **[!UICONTROL Add an API]** window, select **[!UICONTROL Adobe Analytics]**.

   ![](assets/do-not-localize/adobe_io_2.png)

1. 認証のタイプとして「**[!UICONTROL Service Account (JWT)]**」を選択します。

   ![](assets/do-not-localize/adobe_io_3.png)

1. If your Client ID was empty, select **[!UICONTROL Generate a key pair]** to create a Public and Private keypair.

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

To add the project credentials in Adobe Campaign, run the following command as &#39;neolane&#39; user on all the containers of the Adobe Campaign instance to insert the **[!UICONTROL Technical Account]** credentials in the instance configuration file.

```
nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID[/Client_Secret[/Base64_encoded_Private_Key]]
```

>[!NOTE]
>
>秘密鍵は base64 UTF-8 形式でエンコードする必要があります。秘密鍵でない場合は、鍵をエンコードする前に、鍵から新しい行を削除してください。秘密鍵は、統合の作成に使用したものと同じである必要があります。

## 手順 3：pipelined タグを更新 {#update-pipelined-tag}

To update [!DNL pipelined] tag, you need to update the authentication type to Adobe I/O project in the configuration file **config-&lt; instance-name >.xml** as follows:

```
<pipelined ... authType="imsJwtToken"  ... />
```
