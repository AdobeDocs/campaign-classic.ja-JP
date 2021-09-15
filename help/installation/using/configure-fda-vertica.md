---
product: campaign
title: Verticaへのアクセスの設定
description: FDAでVerticaへのアクセスを設定する方法を説明します。
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 8b2a9c73-807a-4936-9fd6-9d26c805a31f
source-git-commit: 0cfe8439007b56014eba497c511904c4f11b39ce
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 19%

---

# Verticaへのアクセスの設定 {#configure-fda-vertica}

![](../../assets/v7-only.svg)

外部データベースに保存された情報を処理するには、Campaignの&#x200B;**Federated Data Access**(FDA)オプションを使用します。 [!DNL Vertica]へのアクセスを設定するには、以下の手順に従います。

1. [CentOS](#vertica-centos)、[Windows](#vertica-windows)または[Debian](#vertica-debian)に[!DNL Vertica]を設定します。
1. Campaignで[!DNL Vertica] [外部アカウント](#vertica-external)を設定します


>[!NOTE]
>
>[!DNL Vertica] コネクタは、ハイブリッドおよびオンプレミスのデプロイメントで使用できます。詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Vertica on CentOS {#vertica-centos}

CentOSで[!DNL Vertica]を設定するには、次の手順に従います。

1. [!DNL Vertica] 用の ODBC ドライバーをダウンロードします。[ここをク](https://www.vertica.com/download/vertica/client-drivers/) リックし、最新のLinux RPMをダウンロードします。

1. その後、次のコマンドを使用してunixODBCをインストールする必要があります。

   ```
   yum search unixODBC
   yum install unixODBC.x86_64
   ```

1. [!DNL Vertica]サーバーを以前にインストールしている場合は、ODBCドライバーが既にインストールされています。 この場合は、次の手順でドライブを更新します。

   ```
   #Switch to root
   sudo su
   
   #Install the package (add --force to update it)
   rpm -Uvh vertica-client-x.x.x-x.x86_64.rpm [--force]
   
   #Open odbcinst.ini
   vi /etc/odbcinst.ini
   
   #Add a section for Vertica and save
   [Vertica]
   Description = Vertica ODBC Driver
   Driver = /opt/vertica/lib64/libverticaodbc.so
   
   #Open odbc.ini
   vi /etc/odbc.ini
   
   #Add your DSN in ODBC Data Sources section, for example:
   [ODBC Data Sources]
   VMart = "VMart database on Vertica"
   
   #Add a DSN definition section below, for example:
   [VMart]
   Description = Vmart Database
   Driver = Vertica
   Database = VMart
   Servername = # The name of the server where Vertica is installed. Use localhost if Vertica is installed on the same machine.
   UID = dbadmin
   PWD = <password>
   Port = 5433
   
   #Cleanup
   #Remove the ODBC package
   rm vertica-client-x.x.x-x.x86_64.rpm
   ```

1. Adobe Campaignでは、[!DNL Vertica]外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[この節](#vertica-external)を参照してください。

## Vertica（Windowsの場合） {#vertica-windows}

1. [Windows 用の ODBC ドライバー](https://www.vertica.com/download/vertica/client-drivers/)をダウンロードします。Windows用のドライバをインストールするには、.NET Framework 3.5を有効にする必要があります。有効にしないと、インストールウィザードが自動的に有効にしてダウンロードを試みます。

1. WindowsでODBCドライバーを設定します。 詳しくは、[このページ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientODBC/SettingUpADSN.htm)を参照してください。

1. Adobe Campaignでは、[!DNL Vertica]外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[この節](#vertical-external)を参照してください。

## Vertica on Debian {#vertica-debian}

1. [!DNL Vertica] 用の ODBC ドライバーをダウンロードします。[ここをクリック](https://sfc-repo.snowflakecomputing.com/odbc/linux/latest/index.html)して、ダウンロードを開始します。

1. その後、次のコマンドを使用してunixODBCをインストールする必要があります。

   ```
   apt-get install unixODBC
   ```

1. [!DNL Vertica]サーバーを以前にインストールしている場合は、ODBCドライバーが既にインストールされています。 この場合は、次の手順でドライブを更新します。

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
   
   #Add a section for Vertica and save
   [Vertica]
   Description = Vertica ODBC Driver
   Driver = /opt/vertica/lib64/libverticaodbc.so
   
   #Open odbc.ini
   vi /etc/odbc.ini
   
   #Add your DSN in ODBC Data Sources section, for example:
   [ODBC Data Sources]
   VMart = "VMart database on Vertica"
   
   #Add a DSN definition section below, for example:
   [VMart]
   Description = Vmart Database
   Driver = Vertica
   Database = VMart
   Servername = # The name of the server where Vertica is installed. Use localhost if Vertica is installed on the same machine.
   UID = dbadmin
   PWD = <password>
   Port = 5433
   ```

1. Adobe Campaignでは、[!DNL Vertica]外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[この節](#vertica-external)を参照してください。

## Vertica外部アカウント {#vertica-external}

Campaignインスタンスを[!DNL Vertica]外部データベースに接続するには、[!DNL Vertica]外部アカウントを作成する必要があります。

1. Campaignの&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;で、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Vertica]**&#x200B;外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Vertica Analytics]

   * **[!UICONTROL サーバー]**：[!DNL Vertica] サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前
   ![](assets/vertica.png)
