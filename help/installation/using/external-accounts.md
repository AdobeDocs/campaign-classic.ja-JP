---
title: 外部アカウント
description: 外部アカウントの作成方法
page-status-flag: never-activated
uuid: e06e7a36-b449-4ab0-a4f6-fa82dbb8de11
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: administration-basics
discoiquuid: da60b9ca-4b51-4bff-affc-2b12c576973a
translation-type: tm+mt
source-git-commit: 99d766cb6234347ea2975f3c08a6ac0496619b41
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 92%

---


# 外部アカウント{#external-accounts}

Adobe Campaign には、事前定義済みの外部アカウントのセットが付属します。外部システムとの接続を設定するために、新しい外部アカウントを作成できます。

外部アカウントは、テクニカルワークフローやキャンペーンワークフロー等の技術プロセスで使用されます。ワークフローのファイル転送や、その他のアプリケーション（Adobe Target、Experience Manager など）とのデータ交換をセットアップする際には外部アカウントを選択する必要があります。

次のタイプの外部アカウントをセットアップできます。

* [ルーティング外部アカウント](#routing-external-account)
* [FTP 外部アカウント](#ftp-external-account)
* [外部データベース外部アカウント](#external-database-external-account)
* [Web 分析の外部アカウント](#web-analytics-external-account)
* [Facebook Connect 外部アカウント](#facebook-connect-external-account)
* [実行インスタンス外部アカウント](#execution-instance-external-account)
* [Adobe Experience Cloud 外部アカウント](#adobe-experience-cloud-external-account)
* [SFTP 外部アカウント](#sftp-external-account)
* [Adobe Experience Manager の外部アカウント](#adobe-experience-manager-external-account)
* [Amazon Simple Storage Service（S3）外部アカウント](#amazon-simple-storage-service--s3--external-account)
* [Microsoft Dynamics CRM 外部アカウント](#microsoft-dynamics-crm-external-account)
* [Oracle On Demand 外部アカウント](#oracle-on-demand-external-account)
* [Salesforce CRM 外部アカウント](#salesforce-crm-external-account)

## 外部アカウントの作成 {#creating-an-external-account}

新しい外部アカウントを作成するには、次の手順に従います。 詳細な設定は、外部アカウントの種類に応じて異なります。

1. From Campaign **[!UICONTROL Explorer]**, select **[!UICONTROL Administration]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL External accounts]**.

   ![](assets/ext_account_1.png)

1. 「**[!UICONTROL 新規]**」ボタンをクリックします。

   ![](assets/ext_account_2.png)

1. Enter a **[!UICONTROL Label]** and an **[!UICONTROL Internal Name]**.
1. 作成したい外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;を選択します。
1. 選択した外部アカウントタイプに応じて資格情報を指定し、アカウントへのアクセスを設定します。

   必要な情報は通常、接続しているサーバーのプロバイダーから提供されます。

1. 「 **[!UICONTROL 有効]** 」オプションを選択して接続をアクティブにします。
1. 「**[!UICONTROL 保存]**」をクリックします。

外部アカウントが作成され、外部アカウントリストに追加されます。

## バウンスメール外部アカウント {#bounce-mails-external-account}

**バウンスメール**&#x200B;外部アカウントで、電子メールサービスの接続に使用する外部 POP3 アカウントを指定します。この外部アカウントについて詳しくは、この[ページ](../../workflow/using/inbound-emails.md)を参照してください。

POP3 アクセス用に設定されたすべてのサーバーは、返信メールの受信に使用できます。

![](assets/ext_account_6.png)

**[!UICONTROL バウンスメール（defaultPopAccount）]**&#x200B;外部アカウントを設定するには、次の手順を実行します。

* **[!UICONTROL サーバー]**

   POP3 サーバーの URL。

* **[!UICONTROL ポート]**

   POP3 接続のポート番号デフォルトのポート番号は 110 です。

* **[!UICONTROL アカウント]**

   ユーザーの名前。

* **[!UICONTROL パスワード]**

   アカウントのパスワード

* **[!UICONTROL 暗号化]**

   **[!UICONTROL デフォルト]**、**[!UICONTROL POP3 + STARTTLS]**、**[!UICONTROL POP3]** または **[!UICONTROL POP3S]** から選択した暗号化のタイプ。

## ルーティング外部アカウント {#routing-external-account}

**[!UICONTROL ルーティング]**&#x200B;外部アカウントを使用すると、インストールしているパッケージに応じて、Adobe Campaign で利用可能な各チャネルを設定できます。

![](assets/ext_account_7.png)

以下のチャネルを設定できます。

* [E メール](../../installation/using/deploying-an-instance.md#email-channel-parameters)
* [モバイル (SMS)](../../delivery/using/sms-channel.md#creating-an-smpp-external-account)
* [電話](../../delivery/using/steps-about-delivery-creation-steps.md#other-channels)
* [ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)
* [エージェンシー](../../delivery/using/steps-about-delivery-creation-steps.md#other-channels)
* [Facebook](../../social/using/publishing-on-facebook-walls.md#delegating-write-access-to-adobe-campaign)
* [Twitter](../../social/using/configuring-publishing-on-twitter.md)
* [iOS チャネル](../../delivery/using/configuring-the-mobile-application.md)
* [Android チャネル](../../delivery/using/configuring-the-mobile-application-android.md)

## FTP 外部アカウント {#ftp-external-account}

FTP 外部アカウントを使用すれば、Adobe Campaign 外でサーバーへのアクセスを設定およびテストできます。外部システム（ファイル転送に使用される FTP サーバー 898 など）との接続をセットアップするために、独自の外部アカウントを作成できます。詳しくは、この[ページ](../../workflow/using/file-transfer.md)を参照してください。

これをおこなうには、この外部アカウントで、FTP サーバーへの接続を確立するために使用するアドレスと資格情報を指定します。

![](assets/ext_account_8.png)

* **[!UICONTROL サーバー]**

   FTP サーバーの名前。

* **[!UICONTROL ポート]**

   FTP 接続のポート番号。デフォルトのポート番号は 21 です。

* **[!UICONTROL アカウント]**

   ユーザーの名前。

* **[!UICONTROL パスワード]**

   アカウントのパスワード

* **[!UICONTROL 暗号化]**

   選択した暗号化のタイプ（**[!UICONTROL なし]**&#x200B;または **[!UICONTROL SSL]**）。

これらの資格情報の見つけ方については、この[ページ](https://help.dreamhost.com/hc/en-us/articles/115000675027-FTP-overview-and-credentials)を参照してください。

## 外部データベース外部アカウント {#external-database-external-account}

外部データベースに接続するには、 **外部データベース** ・タイプ・外部アカウントを使用します。 Federated Data Access(FDA)の詳細については、 [この節を参照してください](../../installation/using/about-fda.md)。

External databases compatible with Campaign are listed in the [Compatibility matrix](../../rn/using/compatibility-matrix.md)

![](assets/ext_account_11.png)

外部アカウント構成の設定は、データベースエンジンによって異なります。 詳しくは、次の節を参照してください。

* [Azure Snapseへのアクセスの構成](../../installation/using/configure-fda-synapse.md)
* Configure access to [Hadoop](../../installation/using/configure-fda-hadoop.md)
* [Oracleへのアクセスの設定](../../installation/using/configure-fda-oracle.md)
* Configure access to [Netezza](../../installation/using/configure-fda-netezza.md)
* [SAP HANAへのアクセスの設定](../../installation/using/configure-fda-sap-hana.md)
* [Snowflakeへのアクセスの設定](../../installation/using/configure-fda-snowflake.md)
* [Sybase IQへのアクセスの構成](../../installation/using/configure-fda-sybase.md)
* Configure access to [Teradata](../../installation/using/configure-fda-teradata.md)

## Web 分析の外部アカウント {#web-analytics-external-account}

**[!UICONTROL Web 分析（Adobe Analytics - データコネクタ）]**&#x200B;外部アカウントを使用すると、ユーザーは Adobe Analytics から Adobe Campaign へとセグメントの形式でデータを転送できます。反対に、Adobe Campaign から配信された E メールキャンペーンの指標と属性を Adobe Analytics - Data コネクタに送信します。

![](assets/ext_account_10.png)

この外部アカウントの場合は、トラッキングされる URL の計算式を強化し、2 つのソリューション間の接続を承認する必要があります。詳しくは、この[ページ](../../platform/using/adobe-analytics-data-connector.md#step-2--create-the-external-account-in-campaign)を参照してください。

## Facebook Connect 外部アカウント {#facebook-connect-external-account}

**[!UICONTROL Facebook Connect]** 外部アカウントがあれば、Facebook アプリケーションにパーソナライズしたコンテンツを表示でき、このソーシャルネットワーク経由で見込み客を獲得しやすくなります。

Facebook アプリケーションごとに、**[!UICONTROL Facebook Connect]** タイプの外部アカウントを作成する必要があります。詳しくは、[ページ](../../social/using/creating-a-facebook-application.md#configuring-external-accounts)を参照してください。

![](assets/ext_account_12.png)

* **[!UICONTROL ホスティングモード]**

   アプリケーションのホスティングモード（「**[!UICONTROL パートナーがホストする]**」または「**[!UICONTROL このインスタンスでホストする]**」）。

* **[!UICONTROL アプリケーション ID]**

   Facebook アプリケーションのアプリ ID。

* **[!UICONTROL アプリケーション秘密鍵]**

   Facebook アプリケーションのアプリケーション秘密鍵。

「このインスタンスでホストする」モードを使用した場合、セキュアキャンバス URL を Facebook の **Facebook Web ゲーム（https）**&#x200B;フィールドに貼り付ける必要があります。

これらの資格情報の見つけ方については、この[ページ](https://developers.facebook.com/docs/facebook-login/access-tokens)を参照してください。

## 実行インスタンス外部アカウント {#execution-instance-external-account}

分割アーキテクチャを使用している場合、コントロールインスタンスにリンクする実行インスタンスを指定し、両者を接続する必要があります。トランザクションメッセージテンプレートは実行インスタンスにデプロイされます。

![](assets/ext_account_13.png)

* **[!UICONTROL URL]**

   実行インスタンスがインストールされているサーバーの URL。

* **[!UICONTROL アカウント]**

   アカウント名、オペレーターフォルダーで定義されている Message Center エージェントと同じである必要があります。

* **[!UICONTROL パスワード]**

   「オペレーター」フォルダーで定義されたアカウントのパスワード。

この設定について詳しくは、この[ページ](../../message-center/using/creating-a-shared-connection.md#control-instance)を参照してください。

## Adobe Experience Cloud 外部アカウント {#adobe-experience-cloud-external-account}

Adobe ID を使用して Adobe Campaign コンソールに接続するには、**[!UICONTROL Adobe Experience Cloud（MAC）]**&#x200B;外部アカウントを設定する必要があります。

![](assets/ext_account_9.png)

* **[!UICONTROL IMS サーバー]**

   IMS サーバーの URL。また、ステージングと本番用のインスタンスがいずれも、同じ IMS 本番エンドポイントを指していることを確認します。

* **[!UICONTROL IMS スコープ]**

   スコープは、IMS によりプロビジョニングされているスコープのサブセットでなければなりません。

* **[!UICONTROL IMS クライアント識別子]**

   IMS クライアントの ID。

* **[!UICONTROL IMS クライアント秘密鍵]**

   IMS クライアント秘密鍵の資格情報。

* **[!UICONTROL コールバックサーバー]**

   Adobe Campaign インスタンスのアクセス URL。

* **[!UICONTROL IMS 組織 ID]**

   IMS 組織の ID。組織 ID を見つけるには、この[ページ](https://docs.adobe.com/content/help/ja-JP/core-services/interface/manage-users-and-products/faq.html)（**IMS 組織 ID はどこにありますか？**）を参照してください。

* **[!UICONTROL 関連付けマスク]**

   このフィールドでは、Enterprise Dashboard の設定名を Adobe Campaign のグループと同期させる構文を定義することができます。

* **[!UICONTROL サーバー]**

   Adobe Experience Cloud インスタンスの URL。

* **[!UICONTROL テナント]**

   Adobe Experience Cloud テナントの名前。

この設定について詳しくは、この[ページ](../../integrations/using/configuring-ims.md)を参照してください。

## SFTP 外部アカウント {#sftp-external-account}

SFTP 外部アカウントを使用すれば、Adobe Campaign 外でサーバーへのアクセスを設定およびテストできます。外部システム（ファイル転送に使用される SFTP など）との接続をセットアップするために、独自の外部アカウントを作成できます。詳しくは、この[ページ](../../workflow/using/file-transfer.md)を参照してください。

![](assets/ext_account_4.png)

* **[!UICONTROL サーバー]**

   SFTP サーバーの URL。

* **[!UICONTROL ポート]**

   FTP 接続のポート番号。デフォルトのポート番号は 22 です。

* **[!UICONTROL アカウント]**

   SFTP サーバーへの接続に使用するアカウント名。

* **[!UICONTROL パスワード]**

   SFTP サーバーへの接続に使用するパスワード。

## Adobe Experience Manager の外部アカウント {#adobe-experience-manager-external-account}

**[!UICONTROL AEM（AEM インスタンス）]**&#x200B;外部アカウントを使用すれば、電子メール配信とフォームのコンテンツを Adobe Experience Manager で直接管理できます。

![](assets/ext_account_5.png)

* **[!UICONTROL サーバー]**

   Adobe Experience Manager サーバーの URL。

* **[!UICONTROL ポート]**

   Adobe Experience Manager オーサリングインスタンスへの接続に使用するアカウント名。

* **[!UICONTROL パスワード]**

   Adobe Experience Manager オーサリングインスタンスへの接続に使用するパスワード。

詳しくは、[この節](../../integrations/using/about-adobe-experience-manager.md)を参照してください。

## Amazon Simple Storage Service（S3）外部アカウント {#amazon-simple-storage-service--s3--external-account}

Amazon Simple Storage Service（S3）コネクタを使用して Adobe Campaign との間でデータのインポートまたはエクスポートをおこなうことができます。コネクタのセットアップはワークフローアクティビティでおこなえます。詳しくは、この[ページ](../../workflow/using/file-transfer.md)を参照してください。

![](assets/ext_account_3.png)

この新規外部アカウントを設定する際には、次の情報を提供する必要があります。

* **[!UICONTROL AWS S3 アカウントサーバー]**

   サーバーの URL。次のように入力する必要があります。

   ```
   <S3bucket name>.s3.amazonaws.com/<s3object path>
   ```

* **[!UICONTROL AWS アクセスキー ID]**

   AWS アクセスキー ID の見つけ方については、この[ページ](https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)を参照してください。

* **[!UICONTROL AWS への秘密アクセスキー]**

   AWS への秘密アクセスキーの見つけ方については、この[ページ](https://aws.amazon.com/jp/blogs/security/wheres-my-secret-access-key/)を参照してください。

* **[!UICONTROL AWS リージョン]**

   AWS リージョンについて詳しくは、この[ページ](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)を参照してください。

* **[!UICONTROL サーバー側の暗号化を使用]**&#x200B;チェックボックスをオンにすると、ファイルを S3 暗号モードで保存できます。

アクセスキー ID および秘密アクセスキーの見つけ方については、Amazon Web サービス[ドキュメント](https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)を参照してください。

## Microsoft Dynamics CRM 外部アカウント {#microsoft-dynamics-crm-external-account}

**[!UICONTROL Microsoft Dynamics CRM]** 外部アカウントがあれば、Microsoft Dynamics データを Adobe Campaign にインポートおよびエクスポートできます。

Adobe Campaign で Microsoft Dynamics コネクタを動作させるための設定は、デプロイメントタイプによって異なります。
**[!UICONTROL オンプレミス]**&#x200B;および **[!UICONTROL Office 365]** のデプロイメントタイプでは、以下の詳細を指定する必要があります。

![](assets/ext_account_21.png)

* **[!UICONTROL アカウント]**

   Microsoft CRM へのログインに使用するアカウント。

* **[!UICONTROL サーバー]**

   Microsoft CRM サーバーの URL。

* **[!UICONTROL パスワード]**

   Microsoft CRM へのログインに使用するパスワード。

* オンプレミスおよび Office 365 用の&#x200B;**[!UICONTROL 会社名]**

   会社の名前。

* オンプレミスデプロイメント用の&#x200B;**[!UICONTROL 組織名]**

   組織の名前。Microsoft Dynamics の開発者向けリソースダッシュボードの「**[!UICONTROL 一意の名前]**」フィールドにある組織名。

* オンプレミス用の **[!UICONTROL CRM バージョン]**

   **[!UICONTROL Dynamics CRM 2007]**、**[!UICONTROL Dynamics CRM 2015]** または **[!UICONTROL Dynamics CRM 2016]** の CRM バージョン。

**[!UICONTROL Web API]** デプロイメントタイプと&#x200B;**[!UICONTROL パスワード資格情報]**&#x200B;認証を使用する場合、以下の詳細を指定する必要があります。

![](assets/ext_account_14.png)

* **[!UICONTROL アカウント]**

   Microsoft CRM へのログインに使用するアカウント。

* **[!UICONTROL サーバー]**

   Microsoft CRM サーバーの URL。

* **[!UICONTROL クライアント識別子]**

   **[!UICONTROL コードを更新]**&#x200B;カテゴリ、**[!UICONTROL クライアント ID]** フィールドの Microsoft Azure 管理ポータルにあるクライアント ID。

* **[!UICONTROL CRM バージョン]**

   **[!UICONTROL Dynamics CRM 2007]**、**[!UICONTROL Dynamics CRM 2015]** または **[!UICONTROL Dynamics CRM 2016]** の CRM バージョン。

**[!UICONTROL Web API]** デプロイメントタイプと&#x200B;**[!UICONTROL 証明書]**&#x200B;認証を使用する場合、以下の詳細を指定する必要があります。

![](assets/ext_account_22.png)

* **[!UICONTROL サーバー]**

   Microsoft CRM サーバーの URL。

* **[!UICONTROL 秘密鍵 (Base64 エンコード)]**

   Base 64 にエンコードされた秘密鍵

* **[!UICONTROL カスタムキー識別子]**

* **[!UICONTROL キー ID]**

* **[!UICONTROL クライアント識別子]**

   **[!UICONTROL コードを更新]**&#x200B;カテゴリ、**[!UICONTROL クライアント ID]** フィールドの Microsoft Azure 管理ポータルにあるクライアント ID。

* **[!UICONTROL CRM バージョン]**

   **[!UICONTROL Dynamics CRM 2007]**、**[!UICONTROL Dynamics CRM 2015]** または **[!UICONTROL Dynamics CRM 2016]** の CRM バージョン。

この設定について詳しくは、この[ページ](../../platform/using/crm-connectors.md#example-for-microsoft-dynamics)を参照してください。

## Oracle On Demand 外部アカウント {#oracle-on-demand-external-account}

**[!UICONTROL Oracle on demand]** 外部アカウントを使用すれば、Oracle データを Adobe Campaign にインポートおよびエクスポートできます。

![](assets/ext_account_18.png)

Oracle On Demand 外部アカウントを Adobe Campaign で使用できるように設定するには、次の情報を提供する必要があります。

* **[!UICONTROL アカウント]**

   Oracle CRM On Demand へのログインに使用するアカウント。

* **[!UICONTROL サーバー]**

   Oracle CRM On Demand サーバーの URL。

* **[!UICONTROL パスワード]**

   Oracle CRM On Demand へのログインに使用するパスワード。

この設定について詳しくは、この[ページ](../../platform/using/crm-connectors.md#example-for-oracle-on-demand)を参照してください。

## Salesforce CRM 外部アカウント {#salesforce-crm-external-account}

**[!UICONTROL Salesforce CRM]** 外部アカウントを使用すれば、Adobe Campaign から Salesforce データをインポートおよびエクスポートできます。

![](assets/ext_account_17.png)

Salesforce CRM 外部アカウントを Adobe Campaign で使用できるように設定するには、次の情報を提供する必要があります。

* **[!UICONTROL アカウント]**

   Salesforce CRM へのログインに使用するアカウント。

* **[!UICONTROL パスワード]**

   Salesforce CRM へのログインに使用するパスワード。

* **[!UICONTROL クライアント識別子]**

   クライアント識別子の見つけ方については、この[ページ](https://help.salesforce.com/articleView?id=000205876&amp;type=1)を参照してください。

* **[!UICONTROL セキュリティトークン]**

   セキュリティトークンの見つけ方については、[ページ](https://help.salesforce.com/articleView?id=000205876&amp;type=1)を参照してください。

* **[!UICONTROL API バージョン]**

   API のバージョン（**[!UICONTROL バージョン 37]**、**[!UICONTROL バージョン 21]** または&#x200B;**[!UICONTROL バージョン 15]**）。

この外部アカウントの場合、設定ウィザードで Salesforce CRM を設定する必要があります。

この設定について詳しくは、この[ページ](../../platform/using/crm-connectors.md#example-for-salesforce-com)を参照してください。
