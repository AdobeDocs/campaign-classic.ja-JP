---
solution: Campaign Classic
product: campaign
title: Adobe Analytics Connector
description: Adobe Analytics Connectorの詳細 プロビジョニング
feature: Overview
role: User, Admin
level: Beginner
exl-id: 24e002aa-4e86-406b-92c7-74f242ee4b86
source-git-commit: 0830e7b8a430fa18bc1326b972741e2e4dc76342
workflow-type: ht
source-wordcount: '591'
ht-degree: 100%

---

# Adobe Analytics Connector のプロビジョニング {#adobe-analytics-connector-provisioning}

![](../../assets/v7-only.svg)

>[!IMPORTANT]
>
> これらの手順は、ハイブリッド実装とオンプレミス実装でのみ実行してください。
>
>ホスト環境での実装については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に問い合わせてください。

Adobe Campaign Classic と Adobe Analytics 間の認証の統合では、Adobe Identity Management サービス（IMS）をサポートしています。Analytics Connector の実装を開始する前に、Adobe IMS を実装し、[Adobe ID を使用して](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/connect-to-campaign/connecting-via-an-adobe-id/about-adobe-id.html?lang=ja) Campaign に接続する必要があります。

この統合が機能するには、Analytics コネクタ専用の Adobe Analytics 製品プロファイルを作成する必要があります。次に、Adobe I/O プロジェクトを作成する必要があります。

## Adobe Analytics 製品プロファイルの作成 {#analytics-product-profile}

製品プロファイルでは、様々な Analytics コンポーネントに対するユーザーのアクセスレベルを指定します。

既に Analytics 製品プロファイルがある場合でも、Analytics コネクタ専用の新しい Adobe Analytics 製品プロファイルを作成する必要があります。これにより、製品プロファイルに、この統合に適した権限が設定されます。

製品プロファイルについて詳しくは、[Admin Console ドキュメント](https://helpx.adobe.com/mt/enterprise/admin-guide.html)を参照してください。

1. [Admin Console](https://adminconsole.adobe.com/) で、Adobe Analytics **[!UICONTROL 製品]**&#x200B;を選択します。

   ![](assets/do-not-localize/triggers_1.png)

1. 「**[!UICONTROL 新規プロファイル]**」をクリックします。

   ![](assets/do-not-localize/triggers_2.png)

1. **[!UICONTROL 製品プロファイル名]**&#x200B;を追加するには、次の構文を使用することをお勧めします。`reserved_campaign_classic_<Company Name>`「**[!UICONTROL 次へ]**」をクリックします。

   この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;は、設定ミスによるエラーを防ぐために、Analytics コネクタにのみ使用してください。

1. 新しく作成した&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を開き、「**[!UICONTROL 権限]**」タブを選択します。

   ![](assets/do-not-localize/triggers_3.png)

1. 「**[!UICONTROL 編集]**」をクリックして様々な機能を設定し、プラス（+）アイコンをクリックして、**[!UICONTROL 製品プロファイル]**&#x200B;に割り当てる権限を選択します。

   権限の管理方法について詳しくは、[Admin Console ドキュメント](https://helpx.adobe.com/mt/enterprise/using/manage-permissions-and-roles.html)を参照してください。

1. **[!UICONTROL レポートスイート]**&#x200B;機能については、後で使用する必要がある&#x200B;**[!UICONTROL レポートスイート]**&#x200B;を追加します。

   レポートスイートがない場合は、[次の手順](../../platform/using/adobe-analytics-connector.md#report-suite-analytics)に従って作成できます。

   ![](assets/do-not-localize/triggers_4.png)

1. **[!UICONTROL 指標]**&#x200B;機能については、後で設定する必要がある&#x200B;**[!UICONTROL 指標]**&#x200B;を追加します。

   必要に応じて、「自動的に含める」オプションをオンにすると、含まれるリストにすべての権限項目が追加され、新しい権限項目が自動的に追加されます。

   ![](assets/do-not-localize/triggers_13.png)

1. **[!UICONTROL ディメンション]**&#x200B;機能については、後で設定する必要がある&#x200B;**[!UICONTROL ディメンション]**&#x200B;を追加します。

1. **[!UICONTROL レポートスイートツール]**&#x200B;機能については、次の権限を追加します。

   * **[!UICONTROL レポートスイート管理]**
   * **[!UICONTROL コンバージョン変数]**
   * **[!UICONTROL 成功イベント]**
   * **[!UICONTROL カスタム Data Warehouse レポート]**
   * **[!UICONTROL データソースマネージャー]**
   * **[!UICONTROL 分類]**

1. **[!UICONTROL Analytics ツール]**&#x200B;機能については、次の権限を追加します。

   * **[!UICONTROL Code Manager - Web サービス]**
   * **[!UICONTROL ログ - Web サービス]**
   * **[!UICONTROL Web サービス]**
   * **[!UICONTROL Web サービスへのアクセス]**
   * **[!UICONTROL 計算指標の作成]**
   * **[!UICONTROL セグメントの作成]**

これで、製品プロファイルが設定されました。 次に、Adobe I/O プロジェクトを作成する必要があります。

## Adobe I/O プロジェクトの作成 {#create-adobe-io}

1. Adobe I/O にアクセスし、IMS 組織の&#x200B;**システム管理者**&#x200B;としてログインします。

   管理者ロールについて詳しくは、[このページ](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html)を参照してください。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。

   ![](assets/do-not-localize/triggers_5.png)

1. 「**[!UICONTROL プロジェクトに追加]**」をクリックし、「**[!UICONTROL API]**」を選択します。

   ![](assets/do-not-localize/triggers_6.png)

1. 「[!DNL Adobe Analytics]」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_7.png)

1. 認証タイプとして「**[!UICONTROL サービスアカウント (JWT)]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_8.png)

1. 「**[!UICONTROL オプション 1 : キーペアを生成]**」オプションを選択し、「**[!UICONTROL キーペアを生成]**」をクリックします。

   config.zip ファイルが自動的にダウンロードされます。

   ![](assets/do-not-localize/triggers_9.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/do-not-localize/triggers_10.png)

1. （[この節](#analytics-product-profile)で説明した）前の手順で作成した&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を選択します。

1. 次に、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   ![](assets/do-not-localize/triggers_11.png)

1. プロジェクトから「[!DNL Adobe Analytics]」を選択し、「**[!UICONTROL サービスアカウント (JWT)]**」下の次の情報をコピーします。

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

   ![](assets/do-not-localize/triggers_12.png)

1. 次のコマンドを使用して、これらのサービスアカウント資格情報を nlserver に貼り付けます。

   ```
   nlserver config -instance:<instanceName> -setimsjwtauth::<ImsOrgId>/<ClientId>/<TechnicalAccountId>/<ClientSecret>/<$(base64 -w0 /path/to/private.key)>
   ```

これで、Analytics コネクタの使用を開始し、顧客の行動をトラッキングできます。
