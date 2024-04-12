---
product: campaign
title: Microsoft SQL Server へのアクセスの設定
description: Microsoft SQL Server へのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
exl-id: 65ab4577-3126-4579-8fcc-e93772ebd1e8
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 8%

---

# Microsoft SQL Server へのアクセスの設定 {#configure-fda-sql}



Campaign の使用 **連合データアクセス** （FDA）外部Microsoft SQL Server データベースに保存された情報を処理するオプション。 へのアクセスを設定するには、次の手順に従います [!DNL Microsoft SQL Server].

1. 設定 [!DNL Microsoft SQL Server] 日付： [CentOS](#sql-centos).
1. 設定 [!DNL Microsoft SQL Server] 日付： [Linux](#sql-linux).
1. 設定 [!DNL Microsoft SQL Server] 日付： [Windows](#sql-windows).
1. の設定 [!DNL Microsoft SQL Server] [外部アカウント](#sql-external) Campaign 内

## CentOS のMicrosoft SQL Server {#sql-centos}

>[!NOTE]
>
> [!DNL Microsoft SQL Server] は CentOS 7 および 6 で使用可能です。

を設定 [!DNL Microsoft SQL Server] centOS では、次の手順に従います。

1. 次のコマンドを使用して、SQL ODBC ドライバをダウンロードしてインストールします。

   ```
   sudo su
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
   exit
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
   sudo ACCEPT_EULA=Y yum install msodbcsql
   ```

1. Adobe Campaignで、以下を設定できます [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#sql-external).

## Microsoft SQL Server on Linux {#sql-linux}

>[!NOTE]
>
> 古いバージョンのAdobe Campaign（7.2.1 以前）を使用している場合は、をインストールする必要があります `unix ODBC drivers`.

1. から MS ODBC ドライバをダウンロードします [このページ](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql17/).

1. root ユーザーとして、次のコマンドを実行します。

   ```
   # install the mssql odbc that was downloaded
   dpkg -i msodbcsql17_17.7.1.1-1_amd64.deb
   # accept the license terms
   ```

1. Adobe Campaignで、以下を設定できます [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#sql-external).

## Windows でのMicrosoft SQL Server {#sql-windows}

を設定 [!DNL Microsoft SQL Server] windows の場合：

1. Windows の場合、次をクリックします。 **[!UICONTROL Campaign コントロールパネル]** &#39;>&#39; **[!UICONTROL システムとセキュリティ]** &#39;>&#39; **[!UICONTROL 管理ツール]**&#39;>&#39; **[!UICONTROL ODBC データソース （64 ビット）]**.

1. から **[!UICONTROL ODBC データソース （64 ビット）]** 新しいウィンドウ、クリック **[!UICONTROL 追加…]**.

1. SQL Server Native Client v11 がに一覧表示されているかどうかを確認します。 **[!UICONTROL 新しいデータソースの作成]** ウィンドウ。

1. SQL Server Native Client が一覧にない場合は、次の場所からダウンロードできます。 [このページ](https://www.microsoft.com/en-my/download/details.aspx?id=36434).

1. Adobe Campaignで、以下を設定できます [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#sql-external).

## Microsoft SQL Server 外部アカウント {#sql-external}

を作成する必要があります [!DNL Microsoft SQL Server] campaign インスタンスをユーザーに接続するための外部アカウント [!DNL Microsoft SQL Server] 外部データベース。

1. Campaign から **[!UICONTROL エクスプローラー]**&#x200B;を選択し、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. 次の下 **[!UICONTROL 設定]**&#x200B;を選択 [!DNL Microsoft SQL Server] から **[!UICONTROL タイプ]** ドロップダウン。

   ![](assets/sql.png)

1. の設定 **[!UICONTROL Microsoft SQL Server]** 外部アカウント認証：

   * **[!UICONTROL サーバー]**：の URL [!DNL Microsoft SQL Server] サーバー。

   * **[!UICONTROL アカウント]**：ユーザーの名前。

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード。

   * **[!UICONTROL データベース]**：データベースの名前（オプション）。

   * **[!UICONTROL Timezone]**：で設定されたタイムゾーン [!DNL Microsoft SQL Server]. [詳細情報](https://docs.microsoft.com/en-us/sql/t-sql/functions/current-timezone-transact-sql?view=sql-server-ver15)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースにAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

1. クリック **[!UICONTROL 保存]** 設定が完了したら、

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| 認証 | コネクターでサポートされている認証のタイプ。 現在サポートされている値：ActiveDirectoryMSI。 <br> 詳しくは、例 8 を参照してください [Microsoft ドキュメント](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory?view=sql-server-ver15#example-connection-strings). |
| 暗号化 | 接続でネットワーク経由の TLS 暗号化を使用するかどうかを指定します。 使用可能な値は次のとおりです **はい/必須（18.0 以降）**, **なし/オプション（18.0 以降）**、および **厳密（18.0 以降）**. デフォルト値はに設定されています。 **はい** バージョン 18.0 以降 **なし** （以前のバージョン）。 <br>詳しくは、次を参照してください [Microsoft ドキュメント](https://docs.microsoft.com/en-us/sql/connect/odbc/dsn-connection-string-attribute?view=azure-sqldw-latest#encrypt). |
| TrustServerCertificate | で使用する場合、自己署名サーバー証明書を使用した暗号化を有効にします **暗号化**. <br>使用できる値： **はい** または **なし** （デフォルト値。サーバー証明書が検証されることを意味します）。 |
