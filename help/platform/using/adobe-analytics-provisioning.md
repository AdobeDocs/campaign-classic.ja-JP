---
solution: Campaign Classic
product: campaign
title: Adobe Analytics コネクタ
description: Adobe Analytics コネクタの詳細 プロビジョニング
feature: Overview
role: User, Admin
level: Beginner
source-git-commit: 24cd84d37c48613aa035769514a43b6dd7aa3869
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 7%

---

# Adobe Analytics Connectorのプロビジョニング {#adobe-analytics-connector-provisioning}

![](../../assets/common.svg)

>[!IMPORTANT]
>
> これらの手順は、ハイブリッド実装とオンプレミス実装のみで実行する必要があります。
>
>ホスト型実装の場合は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)チームにお問い合わせください。

Adobe Campaign Classic認証とAdobe Analytics認証の統合は、AdobeIdentity Managementサービス(IMS)をサポートします。 Analyticsコネクタの実装を開始する前に、Adobe IMSを実装し、Adobe ID](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/connect-to-campaign/connecting-via-an-adobe-id/about-adobe-id.html?lang=en)経由でCampaign [に接続する必要があります。

この統合を機能させるには、Analyticsコネクタ専用に使用されるAdobe Analytics製品プロファイルを作成する必要があります。 次に、プロジェクトを作成する必要がありますAdobe I/O。

## Adobe Analytics製品プロファイルの作成 {#analytics-product-profile}

製品プロファイルは、様々なAnalyticsコンポーネントでのユーザーのアクセスレベルを決定します。

既にAnalytics製品プロファイルをお持ちの場合でも、Analyticsコネクタ専用の新しいAdobe Analytics製品プロファイルを作成する必要があります。 これにより、製品プロファイルにこの統合に対する正しい権限が設定されます。

製品プロファイルについて詳しくは、[Admin Consoleのドキュメント](https://helpx.adobe.com/mt/enterprise/admin-guide.html)を参照してください。

1. [Admin console](https://adminconsole.adobe.com/)から、Adobe Analytics **[!UICONTROL 製品]**&#x200B;を選択します。

   ![](assets/do-not-localize/triggers_1.png)

1. 「**[!UICONTROL 新しいプロファイル]**」をクリックします。

   ![](assets/do-not-localize/triggers_2.png)

1. **[!UICONTROL 製品プロファイル名]**&#x200B;を追加するには、次の構文を使用することをお勧めします。`reserved_campaign_classic_<Company Name>`. 次に、「**[!UICONTROL 次へ]**」をクリックします。

   この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;は、設定ミスエラーを防ぐために、Analyticsコネクタにのみ使用する必要があります。

1. 新しく作成した&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を開き、「**[!UICONTROL 権限]**」タブを選択します。

   ![](assets/do-not-localize/triggers_3.png)

1. 「**[!UICONTROL 編集]**」をクリックして様々な機能を設定し、プラス(+)アイコンをクリックして、**[!UICONTROL 製品プロファイル]**&#x200B;に割り当てる権限を選択します。

   権限の管理方法について詳しくは、[Admin Consoleのドキュメント](https://helpx.adobe.com/mt/enterprise/using/manage-permissions-and-roles.html)を参照してください。

1. **[!UICONTROL レポートスイート]**&#x200B;機能の場合は、後で使用する必要がある&#x200B;**[!UICONTROL レポートスイート]**&#x200B;を追加します。

   レポートスイートがない場合は、[次の手順](../../platform/using/adobe-analytics-connector.md#report-suite-analytics)に従って作成できます。

   ![](assets/do-not-localize/triggers_4.png)

1. **[!UICONTROL Metrics]**&#x200B;機能の場合は、後で&#x200B;**[!UICONTROL Metrics]**&#x200B;を設定する必要があります。

   必要に応じて、「自動含める」オプションをオンにすると、含まれるリストにすべての権限項目が追加され、新しい権限項目が自動的に追加されます。

   ![](assets/do-not-localize/triggers_13.png)

1. **[!UICONTROL Dimension]**&#x200B;機能には、後で設定する必要がある&#x200B;**[!UICONTROL Dimension]**&#x200B;を追加します。

1. **[!UICONTROL レポートスイートツール]**&#x200B;機能に、次の権限を追加します。

   * **[!UICONTROL レポートスイート管理]**
   * **[!UICONTROL コンバージョン変数]**
   * **[!UICONTROL 成功イベント]**
   * **[!UICONTROL カスタムData Warehouseレポート]**
   * **[!UICONTROL データソースマネージャー]**
   * **[!UICONTROL 分類]**

1. **[!UICONTROL Analyticsツール]**&#x200B;機能に、次の権限を追加します。

   * **[!UICONTROL コードマネージャー — Webサービス]**
   * **[!UICONTROL ログ — Webサービス]**
   * **[!UICONTROL Webサービス]**
   * **[!UICONTROL Webサービスへのアクセス]**
   * **[!UICONTROL 計算指標の作成]**
   * **[!UICONTROL セグメントの作成]**

これで、製品プロファイルが設定されました。 次に、プロジェクトを作成する必要がありますAdobe I/O。

## Adobe I/Oプロジェクト {#create-adobe-io}

1. Adobe I/Oにアクセスし、IMS組織の&#x200B;**システム管理者**&#x200B;としてログインします。

   管理者の役割について詳しくは、この[ページ](https://helpx.adobe.com/enterprise/using/admin-roles.html)を参照してください。

1. 「**[!UICONTROL 新しいプロジェクトを作成]**」をクリックします。

   ![](assets/do-not-localize/triggers_5.png)

1. 「**[!UICONTROL プロジェクトに追加]**」をクリックし、「**[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/triggers_6.png)

1. [!DNL Adobe Analytics]を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_7.png)

1. 認証の種類として「**[!UICONTROL サービスアカウント(JWT)]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_8.png)

1. **[!UICONTROL オプション1を選択します。「キーペア]**」オプションを生成し、「**[!UICONTROL キーペアを生成]**」をクリックします。

   config.zipファイルが自動的にダウンロードされます。

   ![](assets/do-not-localize/triggers_9.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_10.png)

1. この[節](#analytics-product-profile)で説明した前の手順で作成した&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を選択します。

1. 次に、「**[!UICONTROL 設定済みAPIを保存]**」をクリックします。

   ![](assets/do-not-localize/triggers_11.png)

1. プロジェクトから [!DNL Adobe Analytics] を選択し、「**[!UICONTROL サービスアカウント (JWT)]**」下に次の情報をコピーします。

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

   ![](assets/do-not-localize/triggers_12.png)

1. 次のコマンドを使用して、これらのサービスアカウント資格情報をnlserverに貼り付けます。

   ```
   nlserver config -instance:<instanceName> -setimsjwtauth::<ImsOrgId>/<ClientId>/<TechnicalAccountId>/<ClientSecret>/<$(base64 -w0 /path/to/private.key)>
   ```

これで、Analyticsコネクタの使用を開始し、顧客行動を追跡できます。
