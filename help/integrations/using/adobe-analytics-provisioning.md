---
product: campaign
title: Adobe Analytics コネクタプロビジョニング
description: Adobe Analytics コネクタプロビジョニングの詳細
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="v7 のオンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
feature: Analytics Integration
role: User, Admin
level: Beginner
exl-id: 24e002aa-4e86-406b-92c7-74f242ee4b86
source-git-commit: 84e6b2fad97f0ca5d6621cff4648e0be0bef7521
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 94%

---

# Adobe Analytics コネクタのプロビジョニング {#adobe-analytics-connector-provisioning}

>[!CAUTION]
>
> これらの手順は、ハイブリッド実装とオンプレミス実装でのみ実行してください。
>
>ホスト環境および Campaign Managed Services での実装については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)チームにお問い合わせください。

Adobe Campaign Classic と Adobe Analytics 間の認証の統合では、Adobe Identity Management サービス（IMS）をサポートしています。

* 移行した外部アカウントを管理している場合は、Adobe IMS を実装し、Adobe ID を介して Adobe Campaign に接続する必要があります。

  Adobe ID IMS でログインしたユーザーは、Adobe Analytics の&#x200B;**データコネクタ**&#x200B;アカウントの所有者であり、[以下](#analytics-product-profile)に説明する&#x200B;**製品プロファイル**&#x200B;に対する権限を持っている必要があります。

データコネクタの所有者が、Campaign にログインして Analytics との統合を試行しているユーザーとは異なるユーザーであることが問題でした。

* 新しいコネクタを実装する場合、Adobe IMS の実装はオプションです。Adobe ID ユーザーがいない場合、Adobe Campaign はテクニカルユーザーを使用して Adobe Analytics と同期します。

この統合が機能するには、Analytics コネクタ専用の Adobe Analytics 製品プロファイルを作成する必要があります。次に、Developer Console プロジェクトを作成する必要があります。

>[!AVAILABILITY]
>
> サービスアカウント（JWT）資格情報はアドビによって廃止され、アドビのソリューションおよびアプリとの Campaign 統合では、OAuth サーバー間の資格情報に依存する必要があります。</br>
>
> * Campaign とのインバウンド統合を実装している場合は、[このドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#_blank)の詳細な説明に従ってテクニカルアカウントを移行する必要があります。既存の[サービスアカウント（JWT）資格情報](oauth-technical-account.md)は、2025年6月30日（PT）まで引き続き機能します。</br>
>
> * Campaign と Analytics の統合やExperience Cloud トリガーの統合などのアウトバウンド統合を実装している場合、2025 年 6 月 30 日（PT）まで引き続き機能します。 ただし、この日付までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。

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

   レポートスイートがない場合は、[次の手順](../../integrations/using/gs-aa.md)に従って作成できます。

   ![](assets/do-not-localize/triggers_4.png)

1. **[!UICONTROL 指標]**&#x200B;機能については、後で設定する必要がある&#x200B;**[!UICONTROL 指標]**&#x200B;を追加します。

   必要に応じて、「自動的に含める」オプションをオンにすると、含まれるリストにすべての権限項目が追加され、新しい権限項目が自動的に追加されます。

   ![](assets/do-not-localize/triggers_13.png)

1. **[!UICONTROL ディメンション]**&#x200B;機能については、将来の設定に必要な&#x200B;**[!UICONTROL ディメンション]**&#x200B;を追加します。

   選択したディメンションが外部アカウントで設定するディメンションと一致し、Adobe Analytics の対応する eVar の数と一致していることを確認します。

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

これで、製品プロファイルが設定されました。 次に、OAuth プロジェクトを作成する必要があります。

## OAuth プロジェクトの作成 {#create-adobe-io}

Adobe Analytics コネクタの設定に進むには、Adobe Developer Console にアクセスして、OAuth サーバー間プロジェクトを作成します。

詳細なドキュメントについては、[このページ](oauth-technical-account.md#oauth-service)を参照してください。

## 設定と使用法 {#adobe-analytics-connector-usage}

Adobe CampaignとAdobe Analyticsの操作方法については、[Adobe Campaign v8 ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/connect/ac-aa){target="_blank"} を参照してください。