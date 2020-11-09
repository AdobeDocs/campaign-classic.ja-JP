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
source-git-commit: 8486213403bf848f1632aff06f3f1528b199f86d
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---


# Configuring Adobe I/O for Adobe Experience Cloud Triggers {#configuring-adobe-io}

>[!CAUTION]
>
>oAuth認証を通じて古いバージョンのTriggers統合を使用する場合は、以下 **の説明に従ってAdobeI/Oに移行する必要があります**。 従来のoAuth認証モードは、2021年4月30日に廃止されます。 [詳細情報](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md)

## 前提条件 {#adobe-io-prerequisites}

この実装を開始する前に、以下の点を確認してください。

* adobe campaignの最新バージョン（20.2.1以降）、
* 有効なIMSOrgID:identity managementシステム(IMS)の組織識別子は、Adobe Experience Cloud内の一意の識別子です。この識別子は、VisitorIDサービスやIMSシングルサインオン(SSO)などに使用されます。
* IMS組織への開発者アクセス権。

>[!NOTE]
>
>IMS組織のシステム管理者権限を要求する必要がある場合は、このページ [で詳しく説明する手順に従って](https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/manage-developers.ug.html) 、すべての製品プロファイルにこのアクセス権を与えます。


## 手順1:AdobeI/Oプロジェクトの作成/更新 {#creating-adobe-io-project}

1. AdobeI/Oにアクセスし、IMSorgのシステム管理者権限でログインします。

   >[!NOTE]
   >
   > 正しいIMSorgポータルにログインしていることを確認します。

1. 既存の統合クライアントIDをインスタンス設定ファイルims/authIMSTAClientIdから抽出します。 既存の属性または空の属性は、クライアントIDが設定されていないことを示します。

   >[!NOTE]
   >
   >クライアントIDが空の場合は、AdobeI/Oで直接 **[!UICONTROL 新しいプロジェクト]** を作成できます。

1. 抽出したクライアントIDを使用して、既存のプロジェクトを識別します。 前の手順で抽出したものと同じクライアントIDを持つ既存のプロジェクトを探します。

   ![](assets/do-not-localize/adobe_io_8.png)

1. 「 **[!UICONTROL +」を選択して「プロジェクト]** 」を選択し、「 **[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/adobe_io_1.png)

1. API **[!UICONTROL 追加ウィンドウで、]** Adobe Analyticsを選択します ****。

   ![](assets/do-not-localize/adobe_io_2.png)

1. 認証の種類として「 **[!UICONTROL サービスアカウント(JWT)]** 」を選択します。

   ![](assets/do-not-localize/adobe_io_3.png)

1. クライアントIDが空の場合は、「キーペアを **[!UICONTROL 生成]** 」を選択して、公開キーペアと秘密鍵キーペアを作成します。

   ![](assets/do-not-localize/adobe_io_4.png)

1. 公開鍵をアップロードし、「 **[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_5.png)

1. 「 **Analytics-&lt;組織名>」という製品プロファイルを選択し、** 「設定したAPIを **[!UICONTROL 保存]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_6.png)

1. プロジェクトから、「 **[!UICONTROL サービスアカウント(JWT)]** 」を選択し、次の情報をコピーします。
   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアントシークレット]**
   * **[!UICONTROL テクニカルアカウントID]**
   * **[!UICONTROL 組織ID]**

   ![](assets/do-not-localize/adobe_io_7.png)

## 手順2:Adobe Campaign追加内のプロジェクト資格情報 {#add-credentials-campaign}

Adobe Campaignにプロジェクト資格情報を追加するには、Adobe Campaignインスタンスのすべてのコンテナで&#39;neolane&#39; userとして次のコマンドを実行し、 **[!UICONTROL テクニカルアカウント]** 資格情報をインスタンス設定ファイルに挿入します。

```
nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID[/Client_Secret[/Base64_encoded_Private_Key]]
```

>[!NOTE]
>
>秘密鍵はbase64 UTF-8形式でエンコードする必要があります。 秘密鍵を除き、エンコードする前に、鍵から新しい行を削除してください。 秘密鍵は、統合の作成に使用したものと同じである必要があります。

## 手順3:パイプラインタグの更新 {#update-pipelined-tag}

タグを更新するに [!DNL pipelined] は、次のように、設定ファイル **config-&lt; instance-name >.xml** :

```
<pipelined ... authType="imsJwtToken"  ... />
```
