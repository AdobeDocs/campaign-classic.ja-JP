---
product: campaign
title: 外部アカウント
description: 外部アカウントの作成方法を説明します
audience: platform
content-type: reference
topic-tags: administration-basics
exl-id: 4a17d5e8-c73f-42e7-b641-0fee6a52c5c0
source-git-commit: 31a475c98b09bbeca6a16c6fd98698af10016033
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 78%

---

# 外部アカウント{#external-accounts}

![](../../assets/v7-only.svg)

Adobe Campaign には、事前に定義された一連の外部アカウントが付属しています。外部システムとの接続を設定する場合は、新しい外部アカウントを作成します。

外部アカウントは、テクニカルワークフローやキャンペーンワークフローなどの技術プロセスで使用されます。例えば、ワークフローにおけるファイル転送や、他のアプリケーション（Adobe Target、Experience Manager など）とのデータ交換などをセットアップする場合、外部アカウントを選択する必要がありす。

## 外部アカウントの作成 {#creating-an-external-account}

新しい外部アカウントを作成するには、次の手順に従います。 詳細な設定は、外部アカウントのタイプによって異なります。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;を選択します。 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

   ![](assets/ext_account_1.png)

1. 「**[!UICONTROL 新規]**」ボタンをクリックします。

   ![](assets/ext_account_2.png)

1. を入力します。 **[!UICONTROL ラベル]** および **[!UICONTROL 内部名]**.
1. 作成したい外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;を選択します。
1. 選択した外部アカウントタイプに応じて資格情報を指定し、アカウントへのアクセスを設定します。

   必要な情報は通常、接続しているサーバーのプロバイダーから提供されます。

1. 次を確認します。 **[!UICONTROL 有効]** オプションを使用して、接続を有効にします。
1. 「**[!UICONTROL 保存]**」をクリックします。

外部アカウントが作成され、外部アカウントリストに追加されます。

## キャンペーン固有の外部アカウント

### バウンスメール {#bounce-mails-external-account}

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

* **[!UICONTROL 関数]**

   インバウンドメールまたは SOAP ルーター

>[!IMPORTANT]
>
>Microsoft OAuth 2.0 を使用して POP3 外部アカウントを設定する前に、まず Azure portal にアプリケーションを登録する必要があります。詳しくは、[このページ](https://docs.microsoft.com/ja-jp/azure/active-directory/develop/quickstart-register-app)を参照してください。

を使用して POP3 外部を設定するには **Microsoft OAuth 2.0**、 **[!UICONTROL Microsoft OAuth 2.0]** 「 」オプションを選択し、次のフィールドに入力します。

* **[!UICONTROL Azure テナント]**

   Azure ID（またはディレクトリ（テナント）ID）は、Azure portal のアプリケーションの概要の「**初期設定**」ドロップダウンで確認できます。

* **[!UICONTROL Azure クライアント ID]**

   クライアント ID（またはアプリケーション（クライアント）ID）は、Azure portal のアプリケーションの概要の「**初期設定**」ドロップダウンで確認できます。

* **[!UICONTROL Azure Client Secret]**

   クライアントシークレット ID は、Azure portal のアプリケーションの&#x200B;**証明書と秘密鍵**&#x200B;メニューから、「**クライアントシークレット**」列で確認することができます。

* **[!UICONTROL Azure リダイレクト URL]**

   リダイレクト URL は Azure portal のアプリケーションの&#x200B;**認証**&#x200B;メニューで確認することができます。次の構文で `nl/jsp/oauth.jsp` 終わる必要があります。例：`https://redirect.adobe.net/nl/jsp/oauth.jsp`。

別の資格情報を入力した後、**[!UICONTROL 接続の設定]**&#x200B;をクリックして、外部アカウントの設定を完了できます。

### ルーティング{#routing-external-account}

**[!UICONTROL ルーティング]**&#x200B;外部アカウントを使用すると、インストールしているパッケージに応じて、Adobe Campaign で利用可能な各チャネルを設定できます。

![](assets/ext_account_7.png)

以下のチャネルを設定できます。

* [電子メール](../../installation/using/deploying-an-instance.md#email-channel-parameters)
* [モバイル（SMS）](../../delivery/using/sms-set-up.md#creating-an-smpp-external-account)
* [電話](../../delivery/using/steps-about-delivery-creation-steps.md#other-channels)
* [ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)
* [エージェンシー](../../delivery/using/steps-about-delivery-creation-steps.md#other-channels)
* [Twitter](../../social/using/about-social-marketing.md)
* [iOS チャネル](../../delivery/using/configuring-the-mobile-application.md)
* [Android チャネル](../../delivery/using/configuring-the-mobile-application-android.md)

### 実行インスタンス  {#execution-instance-external-account}

分割アーキテクチャを使用している場合、コントロールインスタンスにリンクする実行インスタンスを指定し、両者を接続する必要があります。トランザクションメッセージテンプレートは実行インスタンスにデプロイされます。

![](assets/ext_account_13.png)

* **[!UICONTROL URL]**

   実行インスタンスがインストールされているサーバーの URL。

* **[!UICONTROL アカウント]**

   アカウント名、オペレーターフォルダーで定義されている Message Center エージェントと同じである必要があります。

* **[!UICONTROL パスワード]**

   「オペレーター」フォルダーで定義されたアカウントのパスワード。

この設定について詳しくは、この[ページ](../../message-center/using/configuring-instances.md#control-instance)を参照してください。

## 外部システムの外部アカウントへのアクセス

### FTP {#ftp-external-account}

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

### SFTP {#sftp-external-account}

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

Windows で SSH キーを追加するには：

1. を作成します。 **ホーム** 環境変数に値を設定し、インストールディレクトリに設定します。

2. 秘密鍵を `/$HOME/.ssh/id_rsa` フォルダー。

3. Adobe Campaignサービスを再起動します。

### 外部データベース（FDA） {#external-database-external-account}

以下を使用： **外部データベース** 外部データベースに接続する外部アカウントを入力します。 Federated Data Access（FDA）オプションについて詳しくは、[この節](../../installation/using/about-fda.md)を参照してください。

 Campaign と互換性のある外部データベースは、[互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されています。

![](assets/ext_account_11.png)

外部アカウントの設定は、データベースエンジンによって異なります。 詳しくは、次の節を参照してください。

* へのアクセスの設定 [vertica analytics](../../installation/using/configure-fda-vertica.md)
* へのアクセスの設定 [Snowflake](../../installation/using/configure-fda-snowflake.md)
* へのアクセスの設定 [Google BigQuery](../../installation/using/configure-fda-google-big-query.md)
* へのアクセスの設定 [azure synapse](../../installation/using/configure-fda-synapse.md)
* へのアクセスの設定 [Hadoop](../../installation/using/configure-fda-hadoop.md)
* へのアクセスの設定 [Oracle](../../installation/using/configure-fda-oracle.md)
* へのアクセスの設定 [Netezza](../../installation/using/configure-fda-netezza.md)
* へのアクセスの設定 [SAP HANA](../../installation/using/configure-fda-sap-hana.md)
* へのアクセスの設定 [Snowflake](../../installation/using/configure-fda-snowflake.md)
* へのアクセスの設定 [sybase IQ](../../installation/using/configure-fda-sybase.md)
* へのアクセスの設定 [Teradata](../../installation/using/configure-fda-teradata.md)


## Adobeソリューション統合外部アカウント

### Adobe Experience Cloud {#adobe-experience-cloud-external-account}

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

    組織の ID。組織 ID を見つけるには、 [このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}.

* **[!UICONTROL 関連付けマスク]**

   このフィールドでは、Enterprise Dashboard の設定名を Adobe Campaign のグループと同期させる構文を定義することができます。

* **[!UICONTROL サーバー]**

   Adobe Experience Cloud インスタンスの URL。

* **[!UICONTROL テナント]**

   Adobe Experience Cloud テナントの名前。

この設定について詳しくは、 [このページ](../../integrations/using/configuring-ims.md).

## Web 分析 {#web-analytics-external-account}

この **[!UICONTROL Web 分析]** 外部アカウントを使用すると、Adobe AnalyticsからAdobe Campaignにセグメントの形式でデータを転送できます。 反対に、Adobe Campaignから配信された E メールキャンペーンの指標と属性をAdobe Analyticsコネクタに送信します。

![](assets/ext_account_10.png)

この外部アカウントの場合は、トラッキングされる URL の計算式を強化し、2 つのソリューション間の接続を承認する必要があります。詳しくは、この[ページ](../../platform/using/adobe-analytics-connector.md#external-account-classic)を参照してください。

### Adobe Experience Manager {#adobe-experience-manager-external-account}

**[!UICONTROL AEM（AEM インスタンス）]**&#x200B;外部アカウントを使用すれば、電子メール配信とフォームのコンテンツを Adobe Experience Manager で直接管理できます。

![](assets/ext_account_5.png)

* **[!UICONTROL サーバー]**

   Adobe Experience Manager サーバーの URL。

* **[!UICONTROL ポート]**

   Adobe Experience Manager オーサリングインスタンスへの接続に使用するアカウント名。

* **[!UICONTROL パスワード]**

   Adobe Experience Manager オーサリングインスタンスへの接続に使用するパスワード。

詳しくは、[この節](../../integrations/using/about-adobe-experience-manager.md)を参照してください。

## CRM コネクタの外部アカウント

### Microsoft Dynamics CRM {#microsoft-dynamics-crm-external-account}

>[!NOTE]
>
> **[!UICONTROL オンプレミス]** および **[!UICONTROL Office 365]** デプロイメントタイプは非推奨（廃止予定）になりました。 [詳細情報](../../rn/using/deprecated-features.md)。

**[!UICONTROL Microsoft Dynamics CRM]** 外部アカウントを使用すると、Microsoft Dynamics データを Adobe Campaign に読み込みおよび書き出しできます。

Campaign - Microsoft Dynamics CRM コネクタの詳細については、こちらを参照してください [ページ](../../platform/using/crm-ms-dynamics.md).

**[!UICONTROL Web API]** デプロイメントタイプと&#x200B;**[!UICONTROL パスワード資格情報]**&#x200B;認証を使用する場合、以下の詳細を指定する必要があります。

![](assets/ext_account_14.png)

* **[!UICONTROL アカウント]**

   Microsoft CRM へのログインに使用するアカウント。

* **[!UICONTROL サーバー]**

   Microsoft CRM サーバーの URL。

   Microsoft CRM を検索するには **[!UICONTROL サーバー URL]**、Microsoft Dynamics CRM アカウントにアクセスし、 **Dynamics 365** アプリを選択します。 次に、 **[!UICONTROL サーバー URL]** ブラウザーのアドレスバー（例： ） `https://myserver.crm.dynamics.com/`.

* **[!UICONTROL クライアント識別子]**

   **[!UICONTROL コードを更新]**&#x200B;カテゴリ、**[!UICONTROL クライアント ID]** フィールドの Microsoft Azure 管理ポータルにあるクライアント ID。

* **[!UICONTROL CRM バージョン]**

   選択 **[!UICONTROL Dynamics CRM 365]** CRM バージョン。

**[!UICONTROL Web API]** デプロイメントタイプと&#x200B;**[!UICONTROL 証明書]**&#x200B;認証を使用する場合、以下の詳細を指定する必要があります。

![](assets/ext_account_22.png)

* **[!UICONTROL サーバー]**

   Microsoft CRM サーバーの URL。

   Microsoft CRM を検索するには **[!UICONTROL サーバー URL]**、Microsoft Dynamics CRM アカウントにアクセスし、 **Dynamics 365** アプリを選択します。 次に、 **[!UICONTROL サーバー URL]** ブラウザーのアドレスバー（例： ） `https://myserver.crm.dynamics.com/`.

* **[!UICONTROL 秘密鍵 (Base64 エンコード)]**

   秘密鍵は Base64 にエンコードする必要があります。

   それには、Base64 エンコーダーを利用するか、Linux の場合はコマンドライン `base64 -w0 private.key` を使用します。

* **[!UICONTROL カスタムキー識別子]**

* **[!UICONTROL キー ID]**

* **[!UICONTROL クライアント識別子]**

   **[!UICONTROL コードを更新]**&#x200B;カテゴリ、**[!UICONTROL クライアント ID]** フィールドの Microsoft Azure 管理ポータルにあるクライアント ID。

* **[!UICONTROL CRM バージョン]**

   **[!UICONTROL Dynamics CRM 2007]**、**[!UICONTROL Dynamics CRM 2015]** または **[!UICONTROL Dynamics CRM 2016]** の CRM バージョン。

この設定について詳しくは、この[ページ](../../platform/using/crm-connectors.md)を参照してください。

### Salesforce.com CRM  {#salesforce-crm-external-account}

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

   API のバージョンを選択します。

この外部アカウントの場合、設定ウィザードで Salesforce CRM を設定する必要があります。

この設定について詳しくは、この[ページ](../../platform/using/crm-connectors.md)を参照してください。

## データ外部アカウントの転送

### Amazon Simple Storage Service（S3） {#amazon-simple-storage-service--s3--external-account}

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

### Azure Blob ストレージ {#azure-blob-external-account}

この **Azure Blob ストレージ** 外部アカウントを使用して、 Adobe Campaignにデータをインポートまたはエクスポートできます **[!UICONTROL ファイル転送]** ワークフローアクティビティ。 詳しくは、[この節](../../workflow/using/file-transfer.md)を参照してください。

![](assets/ext_account_23.png)

**** Azure 外部アカウントを Adobe Campaign で使用できるように設定するには、次の情報が必要です。

* **[!UICONTROL サーバー]**

   Azure BLOB ストレージサーバーの URL です。

* **[!UICONTROL 暗号化]**

   選択した暗号化のタイプ（**[!UICONTROL なし]**&#x200B;または **[!UICONTROL SSL]**）。

* **[!UICONTROL アクセスキー]**

   検索場所 **[!UICONTROL アクセスキー]**（これを参照） [ページ](https://docs.microsoft.com/ja-JP/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).
