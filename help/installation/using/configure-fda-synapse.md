---
title: シナプスへのアクセスの設定
description: FDAでのシナプスへのアクセスを構成する方法を学びます。
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: be3626e858ced32e9dbfd5d07da29a4ccf256ac4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 78%

---


# Azure Synapse へのアクセスの設定 {#configure-access-to-azure-synapse}

キャンペーン [Federated Data Access](../../installation/using/about-fda.md) (FDA)オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、Microsoft Azure Synapse Analyticsへのアクセスを構成します。

1. CentOS [、](#azure-centos)Windows [](#azure-windows) 、 [DebianでAzure Synapseを構成します](#azure-debian)
1. キャンペーンでAzure Synapse [外部アカウント](#azure-external) を構成します

## CentOS での Azure Synapse {#azure-centos}

>[!CAUTION]
>
>* ODBCドライバをインストールするには、root権限が必要です。
>* Microsoft が提供する Red Hat Enterprise ODBC ドライバーは、CentOS と組み合わせて SQL Server に接続することもできます。
>* バージョン 13.0 は Red Hat 6 および 7 で動作します。


CentOSでAzure Synapseを構成するには、次の手順に従います。

1. まず、ODBC ドライバーをインストールします。こちらの[ページ](https://www.microsoft.com/en-us/download/details.aspx?id=50420)にあります。

   >[!NOTE]
   >
   >これは、ODBC ドライバーのバージョン 13 専用です。

   ```
   sudo su
   curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
   exit
   # Uninstall if already installed Unix ODBC driver
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
   
   sudo ACCEPT_EULA=Y yum install msodbcsql
   
   sudo ACCEPT_EULA=Y yum install mssql-tools
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   
   # the Microsoft driver expects unixODBC to be here /usr/lib64/libodbc.so.1, so add soft links to the '.so.2' files
   cd /usr/lib64
   sudo ln -s libodbccr.so.2   libodbccr.so.1
   sudo ln -s libodbcinst.so.2 libodbcinst.so.1
   sudo ln -s libodbc.so.2     libodbc.so.1
   
   # Set the path for unixODBC
   export ODBCINI=/usr/local/etc/odbc.ini
   export ODBCSYSINI=/usr/local/etc
   source ~/.bashrc
   
   #Add a DSN information to /etc/odbc.ini
   sudo vi /etc/odbc.ini
   
   #Add the following:
   [Azure Synapse Analytics]
   Driver      = ODBC Driver 13 for SQL Server
   Description = Azure Synapse Analytics DSN
   Trace       = No
   Server      = [insert your server here]
   ```

1. 必要に応じて、次のコマンドを実行して unixODBC 開発ヘッダーをインストールできます。

   ```
   sudo yum install unixODBC-devel
   ```

1. ドライバーをインストールした後、必要に応じて、ODBC ドライバーをテストおよび検証し、データベースにクエリをおこなうことができます。次のコマンドを実行します。

   ```
   /opt/mssql-tools/bin/sqlcmd -S yourServer -U yourUserName -P yourPassword -q "your query" # for example -q "select 1"
   ```

1. In Campaign, you can then configure your [!DNL Azure Synapse] external account. For more on how to configure your external account, refer to [this section](#azure-external).

1. Azure Synapse Analytics は TCP 1433 ポートを通じて通信するので、ファイアウォール上でこのポートを開く必要があります。次のコマンドを使用します。

   ```
   firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="[server_ip_here]/32" port port="1433" protocol="tcp" accept'
   # you can ping your hostname and the ping command will translate the hostname to IP address which you can use here
   ```

   >[!NOTE]
   >
   >Azure Synapse Analytics 側からの通信を許可するには、パブリック IP を許可リストに追加する必要がある場合があります。その場合は、[Azure のドキュメント](https://docs.microsoft.com/ja-jp/azure/azure-sql/database/firewall-configure)を参照してください。

1. iptables の場合は、次のコマンドを実行します。

   ```
   iptables -A OUTPUT -p tcp -d [server_hostname_here] --dport 1433 -j ACCEPT
   ```

## Windows での Azure Synapse {#azure-windows}

>[!NOTE]
>
>これは ODBC ドライバーのバージョン 13 専用ですが、Adobe Campaign Classic では SQL Server Native Client ドライバー 11.0 および 10.0 も使用できます。

Windows で Azure Synaps を設定するには、以下を実行します。

1. まず、Microsoft ODBC ドライバーをインストールします。You can find it in [this page](https://www.microsoft.com/en-us/download/details.aspx?id=50420).

1. 次のファイルを選択してインストールします。

   ```
   your_language\your_architecture\msodbcsql.msi (i.e: English\X64\msodbcsql.msi)
   ```

1. ODBC ドライバーをインストールした後、必要に応じてテストできます。詳しくは、この[ページ](https://docs.microsoft.com/ja-jp/sql/connect/odbc/windows/system-requirements-installation-and-driver-files?view=sql-server-ver15)を参照してください。

1. Campaign Classic では、[!DNL Azure Synapse] 外部アカウントを設定できます。For more on how to configure your external account, refer to [this section](#azure-external).

1. Azure Synapse Analytics は TCP 1433 ポートを通じて通信するので、Windows Defender ファイアウォール上でこのポートを開く必要があります。詳しくは、[Windows のドキュメント](https://docs.microsoft.com/ja-jp/windows/security/threat-protection/windows-firewall/create-an-outbound-program-or-service-rule)を参照してください。

## Debian での Azure Synapse {#azure-debian}

**前提条件：**

* ODBC ドライバーをインストールするには、ルート権限が必要です。
* msodbcsql パッケージをインストールするには、curl が必要です。インストールしていない場合は、次のコマンドを実行します。

   ```
   sudo apt-get install curl
   ```

Debian で Azure Synapse を設定するには、以下を実行します。

1. まず、SQL Server 用の Microsoft ODBC ドライバーをインストールします。次のコマンドを使用して、SQL Server 用の ODBC ドライバー 13.1 をインストールします。

   ```
   sudo su
   curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
   curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
   exit
   sudo apt-get update
   sudo ACCEPT_EULA=Y apt-get install msodbcsql
   ```

1. **sudo apt-get update** を呼び出すときに、「**メソッドドライバー /usr/lib/apt/methods/https が見つかりません**」というエラーが発生した場合は、以下のコマンドを実行してください。

   ```
   sudo apt-get install apt-transport-https ca-certificates
   ```

1. 次のコマンドを使用して、mssql-tools をインストールする必要があります。一括コピープログラム（または BCP）ユーティリティを使用してクエリを実行するには、mssq-tools が必要です。

   ```
   sudo ACCEPT_EULA=Y apt-get install mssql-tools
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

1. 必要に応じて、次のコマンドを実行して unixODBC 開発ヘッダーをインストールできます。

   ```
   sudo yum install unixODBC-devel
   ```

1. ドライバーをインストールした後、必要に応じて、ODBC ドライバーをテストおよび検証し、データベースにクエリをおこなうことができます。次のコマンドを実行します。

   ```
   /opt/mssql-tools/bin/sqlcmd -S yourServer -U yourUserName -P yourPassword -q "your query" # for example -q "select 1"
   ```

1. Campaign Classic では、[!DNL Azure Synapse] 外部アカウントを設定できます。For more on how to configure your external account, refer to [this section](#azure-external).

1. Azure Synapse Analytics と確実に接続できるように Debian で iptables を設定するには、次のコマンドを使用して、ホスト名に対してアウトバウンド TCP 1433 ポートを有効にします。

   ```
   iptables -A OUTPUT -p tcp -d [server_hostname_here] --dport 1433 -j ACCEPT
   ```

   >[!NOTE]
   >
   >Azure Synapse Analytics 側からの通信を許可するには、パブリック IP を許可リストに追加する必要がある場合があります。その場合は、[Azure のドキュメント](https://docs.microsoft.com/ja-jp/azure/azure-sql/database/firewall-configure)を参照してください。


## Azure Synapse external account {#azure-external}

[!DNL Azure Synapse] 外部アカウントを使用すれば、Campaign インスタンスを Azure Synapse 外部データベースに接続することができます。

外部アカウントを作成するには、次の手順に従います。 [!DNL Azure Synapse]

1. From Campaign **[!UICONTROL Explorer]**, click **[!UICONTROL Administration]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL External accounts]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

   ![](assets/azure_1.png)

1. [!DNL Azure Synapse] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：Azure Synapse Analytics

   * **[!UICONTROL サーバー]**：Azure Synapse サーバーの URL

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：データベースの名前

