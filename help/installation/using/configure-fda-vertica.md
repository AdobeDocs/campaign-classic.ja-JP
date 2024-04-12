---
product: campaign
title: vertica analyticsへのアクセスの設定
description: FDA でVertica analyticsへのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 8b2a9c73-807a-4936-9fd6-9d26c805a31f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 22%

---

# vertica analyticsへのアクセスの設定 {#configure-fda-vertica}



Campaign の使用 **連合データアクセス** （FDA）外部データベースに保存された情報を処理するオプション。 へのアクセスを設定するには、次の手順に従います [!DNL Vertica Analytics].

1. 設定 [!DNL Vertica Analytics] 日付： [CentOS](#vertica-centos), [Windows](#vertica-windows) または [Debian](#vertica-debian)
1. の設定 [!DNL Vertica Analytics] [外部アカウント](#vertica-external) Campaign 内

![](assets/snowflake_3.png)

## CentOS のVertica analytics {#vertica-centos}

を設定 [!DNL Vertica Analytics] centOS では、次の手順に従います。

1. [!DNL Vertica Analytics] 用の ODBC ドライバーをダウンロードします。[ここをクリック](https://www.vertica.com/download/vertica/client-drivers/) 最新の Linux RPM をダウンロードします。

1. その後、次のコマンドを使用して unixODBC をインストールする必要があります。

   ```
   yum search unixODBC
   yum install unixODBC.x86_64
   ```

1. 以前にをインストールしている場合 [!DNL Vertica Analytics] サーバーに ODBC ドライバーが既にインストールされます。 この場合、ドライブを次のように更新します。

   ```
   #Switch to root
   sudo su
   
   #Install the package (add --force to update it)
   rpm -Uvh vertica-client-x.x.x-x.x86_64.rpm [--force]
   
   #Open odbcinst.ini
   vi /etc/odbcinst.ini
   
   #Add a section for Vertica Analytics and save
   [VerVertica Analyticstica]
   Description = Vertica Analytics ODBC Driver
   Driver = /opt/vertica/lib64/libverticaodbc.so
   
   #Open odbc.ini
   vi /etc/odbc.ini
   
   #Add your DSN in ODBC Data Sources section, for example:
   [ODBC Data Sources]
   VMart = "VMart database on Vertica Analytics"
   
   #Add a DSN definition section below, for example:
   [VMart]
   Description = Vmart Database
   Driver = Vertica Analytics
   Database = VMart
   Servername = # The name of the server where Vertica Analytics is installed. Use localhost if Vertica Analytics is installed on the same machine.
   UID = dbadmin
   PWD = <password>
   Port = 5433
   
   #Cleanup
   #Remove the ODBC package
   rm vertica-client-x.x.x-x.x86_64.rpm
   ```

1. Adobe Campaignで、以下を設定できます [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#vertica-external).

## Windows でのVertica analytics {#vertica-windows}

1. [Windows 用の ODBC ドライバー](https://www.vertica.com/download/vertica/client-drivers/)をダウンロードします。Windows 用ドライバーをインストールするには、.NET Framework 3.5 を有効にする必要があります。有効にしないと、インストール ウィザードによって自動的に有効になり、ダウンロードされます。

1. Windows で ODBC ドライバを設定します。 詳しくは、[このページ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientODBC/SettingUpADSN.htm)を参照してください。

1. Adobe Campaignで、以下を設定できます [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#vertical-external).

## Debian のVertica analytics {#vertica-debian}

1. [!DNL Vertica Analytics] 用の ODBC ドライバーをダウンロードします。[ここをクリック](https://sfc-repo.snowflakecomputing.com/odbc/linux/latest/index.html)して、ダウンロードを開始します。

1. その後、次のコマンドを使用して unixODBC をインストールする必要があります。

   ```
   apt-get install unixODBC
   ```

1. 以前にをインストールしている場合 [!DNL Vertica Analytics] サーバーに ODBC ドライバーが既にインストールされます。 この場合、ドライブを次のように更新します。

   ```
   #Switch to root
   sudo su
   
   #Move or copy the downloaded file and change to /root
   mv vertica_9.3..xx_odbc_x86_64_linux.tar.gz /
   cd /
   
   #Uncompress the file you downloaded
   tar vzxf vertica_9.3..xx_odbc_x86_64_linux.tar.gz
   
   #Remove the tar.gz since it is not needed anymore
   rm vertica_9.3..xx_odbc_x86_64_linux.tar.gz
   
   #Open odbcinst.ini
   vi /etc/odbcinst.ini
   
   #Add a section for Vertica Analytics and save
   [Vertica Analytics]
   Description = Vertica Analytics ODBC Driver
   Driver = /opt/vertica/lib64/libverticaodbc.so
   
   #Open odbc.ini
   vi /etc/odbc.ini
   
   #Add your DSN in ODBC Data Sources section, for example:
   [ODBC Data Sources]
   VMart = "VMart database on Vertica Analytics"
   
   #Add a DSN definition section below, for example:
   [VMart]
   Description = Vmart Database
   Driver = Vertica Analytics
   Database = VMart
   Servername = # The name of the server where Vertica Analytics is installed. Use localhost if Vertica Analytics is installed on the same machine.
   UID = dbadmin
   PWD = <password>
   Port = 5433
   ```

1. Adobe Campaignで、以下を設定できます [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#vertica-external).

## Vertica analytics外部アカウント {#vertica-external}

を作成する必要があります [!DNL Vertica Analytics] campaign インスタンスをユーザーに接続するための外部アカウント [!DNL Vertica Analytics] 外部データベース。

1. Campaign から **[!UICONTROL エクスプローラー]**&#x200B;を選択し、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. の設定 **[!UICONTROL Vertica analytics]** 外部アカウント。次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Vertica Analytics]

   * **[!UICONTROL サーバー]**：[!DNL Vertica Analytics] サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

   ![](assets/vertica.png)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| TimeZoneName | デフォルトでは空で、Campaign Classic アプリケーションサーバーのシステムのタイムゾーンが使用されます。オプションを使用すると、TIMEZONE セッションパラメーターを強制できます。 |

