---
product: campaign
title: Adobe Experience Cloud Triggers 用の Adobe I/O の設定
description: Adobe Experience Cloud Triggers 用の Adobe I/O の設定方法を説明します
audience: integrations
content-type: reference
index: y
internal: n
snippet: y
exl-id: ab30f697-3022-4a29-bbdb-14ca12ec9c3e
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 100%

---

# Adobe Experience Cloud Triggers 用の Adobe I/O の設定{#configuring-adobe-io}

>[!CAUTION]
>
>oAuth 認証を通じて古いバージョンの Triggers 統合を使用する場合は、**以下の説明に従って Adobe I/O に移行する必要があります**。Campaign での従来の OAuth 認証モードは、2021 年 11 月 30 日に廃止される予定です。 [詳細情報](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411)
>
>[!DNL Adobe I/O] へのこうした移行中に、一部の着信トリガーが失われる可能性があることに注意してください。

## 前提条件 {#adobe-io-prerequisites}

この統合は、 **Campaign Classic 20.3、20.2.4、19.1.8 と [!DNL Gold Standard] 11 リリース**&#x200B;以降にのみ適用されます。

この実装を開始する前に、以下の点を確認してください。

* 有効な&#x200B;**組織識別子**：Identity Management システム（IMS）の組織識別子は、Adobe Experience Cloud 内の一意の識別子です。この識別子は、VisitorID サービスや IMS シングルサインオン（SSO）などに使用されます。[詳細情報](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html?lang=ja)
* 組織への&#x200B;**開発者アクセス**。[このページ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)で説明する手順に従い、すべての製品プロファイルに関してこのアクセス権を提供するには、IMS 組織のシステム管理者権限をリクエストする必要があります。

## 手順 1：Adobe I/O プロジェクトの作成と更新 {#creating-adobe-io-project}

1. [!DNL Adobe I/O] にアクセスし、IMS 組織のシステム管理者権限でログインします。

   >[!NOTE]
   >
   > 正しい組織ポータルにログインしていることを確認します。

1. 既存の統合クライアント識別子（クライアント ID） をインスタンス設定ファイル（ims/authIMSTAClientId）から抽出します。属性が存在しないか空の場合は、クライアント識別子が設定されていません。

   >[!NOTE]
   >
   >クライアント識別子が空の場合は、Adobe I/O で直接&#x200B;**[!UICONTROL 新しいプロジェクトを作成]**&#x200B;できます。

1. 抽出したクライアント識別子を使用して、既存のプロジェクトを識別します。前の手順で抽出されたものと同じクライアント識別子を持つ既存のプロジェクトを探します。

   ![](assets/do-not-localize/adobe_io_8.png)

1. 「**[!UICONTROL + プロジェクトに追加]**」を選択して、「**[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/adobe_io_1.png)

1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL Adobe Analytics]**」を選択します。

   ![](assets/do-not-localize/adobe_io_2.png)

1. 認証のタイプとして「**[!UICONTROL Service Account (JWT)]**」を選択します。

   ![](assets/do-not-localize/adobe_io_3.png)

1. クライアント ID が空の場合は、「**[!UICONTROL キーペアを生成]**」を選択して、公開鍵と秘密鍵のペアを作成します。

   キーは、デフォルトの有効期限 365 日で自動的にダウンロードされます。 有効期限が切れたら、新しいキーペアを作成し、設定ファイルで統合を更新する必要があります。 オプション 2 を使用すると、有効期限の長い&#x200B;**[!UICONTROL 公開鍵]**&#x200B;を手動で作成してアップロードすることを選択できます。

   ![](assets/do-not-localize/adobe_io_4.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_5.png)

1. 既存の&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を選択するか、必要に応じて新しいプロファイルを作成します。 この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;には権限は必要ありません。 [!DNL Analytics] **[!UICONTROL 製品プロファイル]**&#x200B;の詳細については、[Adobe Analytics ドキュメント](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=ja#admin-console)を参照してください。

   次に、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   ![](assets/do-not-localize/adobe_io_6.png)

1. プロジェクトから **[!UICONTROL Adobe Analytics]** を選択し、「**[!UICONTROL サービスアカウント (JWT)]**」下に次の情報をコピーします。

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

   ![](assets/do-not-localize/adobe_io_7.png)

>[!CAUTION]
>
>Adobe I/O 証明書は 12 か月後に期限が切れます。毎年新しいキーペアを生成する必要があります。

## 手順 2：Adobe Campaign へのプロジェクト資格情報の追加 {#add-credentials-campaign}

Adobe Campaign にプロジェクト資格情報を追加するには、Adobe Campaign インスタンスのすべてのコンテナで「neolane」ユーザーとして次のコマンドを実行し、**[!UICONTROL テクニカルアカウント]**&#x200B;資格情報をインスタンス設定ファイルに挿入します。

```
nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID/<Client_Secret>/<Base64_encoded_Private_Key>
```

秘密鍵は、Base64 UTF-8 形式でエンコードする必要があります。それには、次の手順に従います。

1. [手順 1：Adobe I/O プロジェクトの作成と更新](#creating-adobe-io-project)で生成された秘密鍵を使用します。秘密鍵は、統合の作成に使用したものと同じである必要があります。

1. コマンド ```base64 ./private.key``` を使用して秘密鍵をエンコードします。

   >[!NOTE]
   >
   >秘密鍵をコピーして貼り付けるときに、余分な行が自動的に追加される場合があります。 これは、秘密鍵をエンコードする前に忘れずに削除してください。

1. 上記で詳述されたコマンドを実行するには、Base64 UTF-8 形式でエンコードされた新しく生成された秘密鍵を使用します。

## 手順 3：パイプライン化されたタグの更新 {#update-pipelined-tag}

[!DNL pipelined] タグを更新するには、設定ファイル（**config-&lt;インスタンス名>.xml**）で、認証タイプを以下のように Adobe I/O プロジェクトに更新する必要があります。

```
<pipelined ... authType="imsJwtToken"  ... />
```
