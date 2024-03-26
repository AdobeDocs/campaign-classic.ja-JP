---
product: campaign
title: vertica analyticsへのアクセスの設定
description: FDA でVertica analyticsへのアクセスを設定する方法
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 8b2a9c73-807a-4936-9fd6-9d26c805a31f
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 23%

---

# vertica analyticsへのアクセスの設定 {#configure-fda-vertica}



キャンペーンを使用 **Federated Data Access** (FDA) 外部データベースに保存された情報を処理するオプション。 次の手順に従って、へのアクセスを設定します。 [!DNL Vertica Analytics].

1. 設定 [!DNL Vertica Analytics] オン [CentOS](#vertica-centos), [Windows](#vertica-windows) または [Debian](#vertica-debian)
1. を設定します。 [!DNL Vertica Analytics] [外部アカウント](#vertica-external) Campaign 内

![](assets/snowflake_3.png)

## CentOS のvertica analytics {#vertica-centos}

を設定するには、以下を実行します。 [!DNL Vertica Analytics] CentOS で、次の手順に従います。

1. [!DNL Vertica Analytics] 用の ODBC ドライバーをダウンロードします。[ここをクリック](https://www.vertica.com/download/vertica/client-drivers/) 最新の Linux RPM をダウンロードします。

1. その後、次のコマンドを使用して unixODBC をインストールする必要があります。

   ```
   yum search unixODBC
   yum install unixODBC.x86_64
   ```

1. 以前に [!DNL Vertica Analytics] サーバー、ODBC ドライバーは既にインストールされています。 この場合、次のようにドライブを更新します。

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

1. Adobe Campaignで、 [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#vertica-external).

## Windows のvertica analytics {#vertica-windows}

1. [Windows 用の ODBC ドライバー](https://www.vertica.com/download/vertica/client-drivers/)をダウンロードします。Windows 用のドライバーをインストールするには、.NET Framework 3.5 を有効にする必要があります。有効にしない場合は、インストールウィザードが自動的に有効にしてダウンロードを試みます。

1. Windows で ODBC ドライバーを設定します。 詳しくは、[このページ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientODBC/SettingUpADSN.htm)を参照してください。

1. Adobe Campaignで、 [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#vertical-external).

## Vertica analytics(Debian) {#vertica-debian}

1. [!DNL Vertica Analytics] 用の ODBC ドライバーをダウンロードします。[ここをクリック](https://sfc-repo.snowflakecomputing.com/odbc/linux/latest/index.html)して、ダウンロードを開始します。

1. その後、次のコマンドを使用して unixODBC をインストールする必要があります。

   ```
   apt-get install unixODBC
   ```

1. 以前に [!DNL Vertica Analytics] サーバー、ODBC ドライバーは既にインストールされています。 この場合、次のようにドライブを更新します。

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

1. Adobe Campaignで、 [!DNL Vertica Analytics] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#vertica-external).

## Vertica analytics外部アカウント {#vertica-external}

次を作成する必要があります： [!DNL Vertica Analytics] Campaign インスタンスを [!DNL Vertica Analytics] 外部データベース。

1. キャンペーンから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. を設定します。 **[!UICONTROL Vertica analytics]** 外部アカウントで、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Vertica Analytics]

   * **[!UICONTROL サーバー]**：[!DNL Vertica Analytics] サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

   ![](assets/vertica.png)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| TimeZoneName | デフォルトでは空で、Campaign Classic アプリケーションサーバーのシステムのタイムゾーンが使用されます。このオプションを使用すると、TIMEZONE セッションパラメーターを強制的に指定できます。 |

