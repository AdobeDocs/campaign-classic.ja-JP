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
source-git-commit: 02eebe83de49ee97e573b0c47ca1fddb2195b991
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Cloud Triggers 用の Adobe I/O の設定 {#configuring-adobe-io}

![](../../assets/v7-only.svg)

>[!CAUTION]
>
>OAuth 認証による旧バージョンのトリガー統合を使用している場合は、以下に説明するように **Adobe I/O に移行する必要があります**。
>[!DNL Adobe I/O] へのこうした移行中に、一部の着信トリガーが失われる可能性があることに注意してください。
>
>Campaign の従来の OAuth 認証モードは、**2021年10月20日**（PT）に廃止されました。ホスト環境では、**2022年5月25日**（PT）まで延長サポートを受けられます。オンプレミス環境またはハイブリッド環境のお客様は、アドビカスタマーケアに連絡してサポートを **2022年5月**&#x200B;まで延長してください。アドビに [OAuth アプリケーションの AppID を伝える](../../integrations/using/configuring-pipeline.md?lang=en#step-optional)必要があります。

## 前提条件 {#adobe-io-prerequisites}

この統合は、**Campaign Classic 20.2.4 以降、19.1.8、Gold Standard 11 リリース**&#x200B;にのみ適用されます。

この実装を開始する前に、以下の点を確認してください。

* 有効な **組織識別子**:組織 ID はAdobe Experience Cloud内の一意の識別子です。VisitorID サービスや IMS シングルサインオン (SSO) などに使用されます。 [詳細情報](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja)
* 組織への&#x200B;**開発者のアクセス**。組織のシステム管理者は、 **1 つの製品プロファイルへの開発者の追加** 手順の詳細 [このページ](https://helpx.adobe.com/enterprise/using/manage-developers.html) 開発者が `Analytics - {tenantID}` 製品に関連付けられたAdobe Analytics製品のトリガープロファイル。

## 手順 1：Adobe I/O プロジェクトの作成と更新 {#creating-adobe-io-project}

1. アクセス [!DNL Adobe I/O] 組織の開発者アクセス権でログインします。

   >[!NOTE]
   >
   > 正しい組織ポータルにログインしていることを確認します。

1. 既存の統合クライアント識別子（クライアント ID） をインスタンス設定ファイル（ims/authIMSTAClientId）から抽出します。存在しない属性または空の属性は、クライアント識別子が設定されていないことを示します。

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

   >[!CAUTION]
   >
   >再度ダウンロードすることができないので、ダウンロードプロンプトが表示されたら、config.zip ファイルを保存してください。

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

>[!NOTE]
>
>[手順1：Adobe I/O プロジェクトの作成／更新](#creating-adobe-io-project)でクライアント識別子が空でなかった場合、この手順は不要です。

秘密鍵は、Base64 UTF-8 形式でエンコードする必要があります。それには、次の手順に従います。

1. [手順 1：Adobe I/O プロジェクトの作成と更新](#creating-adobe-io-project)で生成された秘密鍵を使用します。秘密鍵は、統合の作成に使用したものと同じである必要があります。

1. `base64 ./private.key > private.key.base64` というコマンドを使用して秘密鍵をエンコードします。これにより、base64 コンテンツが新しいファイル `private.key.base64` に保存されます。

   >[!NOTE]
   >
   >秘密鍵をコピーして貼り付けるときに、余分な行が自動的に追加される場合があります。 これは、秘密鍵をエンコードする前に忘れずに削除してください。

1. ファイル `private.key.base64` からコンテンツをコピーします。

1. Adobe Campaign インスタンスがインストールされている各コンテナに SSH 経由でログインし、`neolane` ユーザーとして次のコマンドを実行して Adobe Campaign にプロジェクト資格情報を追加します。これにより、**[!UICONTROL テクニカルアカウント]**&#x200B;資格情報がインスタンス設定ファイルに挿入されます。

   ```
   nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID/<Client_Secret>/<Base64_encoded_Private_Key>
   ```

## 手順 3：パイプラインタグの更新 {#update-pipelined-tag}

>[!NOTE]
>
>[手順 1：Adobe I/O プロジェクトの作成／更新](#creating-adobe-io-project)でクライアント識別子が空でなかった場合、この手順は不要です。

[!DNL pipelined] タグを更新するには、設定ファイル **config-&lt; instance-name >.xml** で、以下のように認証タイプを Adobe I/O プロジェクトに更新する必要があります。

```
<pipelined ... authType="imsJwtToken"  ... />
```

次に、`config -reload` を実行し、[!DNL pipelined] を再起動して変更内容を反映させます。
