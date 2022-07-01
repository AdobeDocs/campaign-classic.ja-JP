---
product: campaign
title: Microsoft SQL Server へのアクセスの設定
description: Microsoft SQL Server へのアクセスを設定する方法を説明します
source-git-commit: 26ae7ff1f0837a9a50057d97b00422a288b9dc7a
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 10%

---

# Microsoft SQL Server へのアクセスの設定 {#configure-fda-sql}

![](../../assets/v7-only.svg)

キャンペーンを使用 **Federated Data Access** (FDA) 外部のMicrosoft SQL Server データベースに保存された情報を処理するオプション。 次の手順に従って、へのアクセスを設定します。 [!DNL Microsoft SQL Server].

1. 設定 [!DNL Microsoft SQL Server] オン [CentOS](#sql-centos).
1. 設定 [!DNL Microsoft SQL Server] オン [Linux](#sql-linux).
1. 設定 [!DNL Microsoft SQL Server] オン [Windows](#sql-windows).
1. の設定 [!DNL Microsoft SQL Server] [外部アカウント](#sql-external) キャンペーン内

## CentOS でのMicrosoft SQL Server {#sql-centos}

>[!NOTE]
>
> [!DNL Microsoft SQL Server] は CentOS 7 および 6 で利用できます。

を設定するには、以下を実行します。 [!DNL Microsoft SQL Server] CentOS で、次の手順に従います。

1. 次のコマンドを使用して、SQL ODBC ドライバーをダウンロードしてインストールします。

   ```
   sudo su
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
   exit
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
   sudo ACCEPT_EULA=Y yum install msodbcsql
   ```

1. Adobe Campaignで、 [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#sql-external).

## Linux 上のMicrosoft SQL Server {#sql-linux}

>[!NOTE]
>
> 古いバージョンのAdobe Campaign（7.2.1 以前）を実行している場合は、をインストールする必要があります。 `unix ODBC drivers`.

1. から MS ODBC ドライバーをダウンロードします。 [このページ](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql17/).

1. 次のコマンドを root ユーザーとして実行します。

   ```
   # install the mssql odbc that was downloaded
   dpkg -i msodbcsql17_17.7.1.1-1_amd64.deb
   # accept the license terms
   ```

1. Adobe Campaignで、 [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#sql-external).

## Windows 上のMicrosoft SQL Server {#sql-windows}

を設定するには、以下を実行します。 [!DNL Microsoft SQL Server] Windows の場合：

1. Windows の場合、 **[!UICONTROL Campaign コントロールパネル]** &#39;>&#39; **[!UICONTROL システムとセキュリティ]** &#39;>&#39; **[!UICONTROL 管理ツール]**&#39;>&#39; **[!UICONTROL ODBC データソース（64 ビット）]**.

1. 次の **[!UICONTROL ODBC データソース（64 ビット）]** 新しいウィンドウ、クリック **[!UICONTROL 追加…]**.

1. SQL Server Native Client v11 が **[!UICONTROL 新しいデータソースを作成]** ウィンドウ

1. SQL Server Native Client が一覧に表示されない場合は、 [このページ](https://www.microsoft.com/en-my/download/details.aspx?id=36434).

1. Adobe Campaignで、 [!DNL Microsoft SQL Server] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#sql-external).

## Microsoft SQL Server 外部アカウント {#sql-external}

次を作成する必要があります： [!DNL Microsoft SQL Server] Campaign インスタンスを [!DNL Microsoft SQL Server] 外部データベース。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. の下 **[!UICONTROL 設定]**&#x200B;を選択します。 [!DNL Microsoft SQL Server] から **[!UICONTROL タイプ]** 」ドロップダウンリストから選択できます。

   ![](assets/sql.png)

1. の設定 **[!UICONTROL Microsoft SQL Server]** 外部アカウント認証：

   * **[!UICONTROL サーバー]**：[!DNL Microsoft SQL Server] サーバーの URL.

   * **[!UICONTROL アカウント]**：ユーザーの名前.

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード.

   * **[!UICONTROL データベース]**:データベースの名前（オプション）。

   * **[!UICONTROL タイムゾーン]**:タイムゾーンの設定 [!DNL Microsoft SQL Server]. [詳細情報](https://docs.microsoft.com/en-us/sql/t-sql/functions/current-timezone-transact-sql?view=sql-server-ver15)

1. 「**[!UICONTROL パラメーター]**」タブをクリックし、「**[!UICONTROL 機能をデプロイ]**」ボタンをクリックして機能を作成します。

   >[!NOTE]
   >
   >すべての関数を使用するには、リモートデータベースでAdobe Campaign SQL 関数を作成する必要があります。 詳しくは、[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

1. クリック **[!UICONTROL 保存]** 設定が完了したら、

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| 認証 | コネクタでサポートされる認証のタイプ。 現在のサポート値：ActiveDirectoryMSI です。 <br> 詳しくは、例 8 /を参照してください。 [Microsoftドキュメント](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory?view=sql-server-ver15#example-connection-strings). |
| 暗号化 | 接続でネットワーク経由で TLS 暗号化を使用するかどうかを指定します。 指定できる値は次のとおりです。 **はい/必須（18.0 以降）**, **いいえ/オプション（18.0 以降）**、および **strict（18.0 以降）**. デフォルト値はに設定されています。 **はい** バージョン 18.0 以降 **いいえ** 以前のバージョンの <br>詳しくは、 [Microsoftドキュメント](https://docs.microsoft.com/en-us/sql/connect/odbc/dsn-connection-string-attribute?view=azure-sqldw-latest#encrypt). |
| TrustServerCertificate | で使用する場合に、自己署名サーバー証明書を使用して暗号化を有効にします **暗号化**. <br>指定できる値： **はい** または **いいえ** （デフォルト値。サーバー証明書が検証されます）。 |

