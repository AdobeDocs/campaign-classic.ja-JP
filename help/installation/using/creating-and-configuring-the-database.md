---
product: campaign
title: データベースの作成と設定
description: データベースの作成と設定
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f40bab8c-5064-40d9-beed-101a9f22c094
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---

# データベースの作成と設定{#creating-and-configuring-the-database}

データベースを作成する場合、Adobe Campaignには次の2つの異なるオプションが用意されています。

1. データベースの作成または再利用：新しいデータベースを作成する場合や、既存のデータベースを再利用する場合は、このオプションを選択します。 [ケース1を参照：データベース](#case-1--creating-recycling-a-database)を作成/再利用します。
1. 既存のデータベースを使用する場合：管理者が空のデータベースを作成済みで、それを使用する場合は、このオプションを選択します。または既存のデータベースの構造を拡張する場合に使用します。 [ケース2を参照：既存のデータベース](#case-2--using-an-existing-database)を使用します。

設定手順は以下で説明します。

>[!CAUTION]
>
>データベース、ユーザー、スキーマの名前は、数字で始めたり、特殊文字を含めたりすることはできません。
>
>これらの操作を実行できるのは、**内部**&#x200B;識別子のみです。 詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## 例1:データベース{#case-1--creating-recycling-a-database}の作成と再利用

データベースの作成または既存のベースの再利用の手順を以下に示します。 一部の設定は、使用するデータベースエンジンによって異なります。

次の手順が関係します。

* [手順1 — データベースエンジンの選択](#step-1---selecting-the-database-engine),
* [手順2 — サーバーへの接続](#step-2---connecting-to-the-server),
* [手順3 — データベースの接続と特性](#step-3---connection-and-characteristics-of-the-database),
* [手順4 — インストールするパッケージ](#step-4---packages-to-install),
* [手順5 — 作成ステップ](#step-5---creation-steps),
* [手順6 — データベースの作成](#step-6---creating-the-database)を参照してください。

### 手順1 — データベースエンジンの選択{#step-1---selecting-the-database-engine}

ドロップダウン・リストからデータベース・エンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サポートされるデータベースは、Campaignの[互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されています。

サーバーを特定し、実行する操作のタイプを選択します。 この場合、**[!UICONTROL データベースを作成またはリサイクル]**&#x200B;します。

![](assets/s_ncs_install_db_oracle_creation01.png)

選択したデータベースエンジンに応じて、サーバ識別情報が異なる場合があります。

* **Oracle**&#x200B;エンジンの場合は、アプリケーションサーバー用に定義された&#x200B;**TNS名**&#x200B;を設定します。
* **PostgreSQL**&#x200B;または&#x200B;**DB2**&#x200B;エンジンの場合、データベースサーバーにアクセスするには、アプリケーションサーバーで定義されたDNS名（またはIPアドレス）を指定する必要があります。
* **Microsoft SQL Server**&#x200B;エンジンの場合は、次を定義する必要があります。データベース・サーバにアクセスするためにアプリケーション・サーバで定義されたDNS名（またはIPアドレス）:**DNS**&#x200B;または&#x200B;**DNS`\<instance>`**（インスタンスモード）

   >[!CAUTION]
   >
   > 20.3以降、Windows NT認証は廃止されます。 **[!UICONTROL SQL Server認証]** は、Microsoft SQL Serverで使用できる唯一の認証モードになりました。[詳細情報](../../rn/using/deprecated-features.md)

   ![](assets/s_ncs_install_db_mssql_creation01.png)

### 手順2 — サーバー{#step-2---connecting-to-the-server}への接続

**[!UICONTROL サーバーアクセス]**&#x200B;ウィンドウで、データベースサーバーアクセスを定義します。

![](assets/s_ncs_install_db_oracle_creation02.png)

これをおこなうには、データベースにアクセスする権限を持つ&#x200B;**管理システムアカウント**&#x200B;の名前とパスワードを入力します。次に例を示します。

* **** システム(Oracleデータベース用)
* **** Microsoft SQL Serverデータベースの場合、
* **** PostgreSQLデータベースのpostgres
* **db2inst1** （DB2データベース用）

### 手順3 — データベースの接続と特性{#step-3---connection-and-characteristics-of-the-database}

次の手順では、データベースにログオンするための設定を指定できます。

![](assets/s_ncs_install_db_oracle_creation03.png)

次の設定を定義する必要があります。

* 作成するデータベースの名前を指定します。

   >[!NOTE]
   >
   >DB2データベースの場合、データベースの名前は8文字以下にする必要があります。

* このデータベースにリンクされているアカウントのパスワードを入力します。
* データベースがUnicodeである必要があるかどうかを示します。

   **[!UICONTROL Unicodeデータベース]**&#x200B;オプションを使用すると、言語に関係なく、すべての文字タイプをUnicodeで保存できます。

   >[!NOTE]
   >
   >oracleデータベースでは、**[!UICONTROL Unicodeストレージ]**&#x200B;オプションを使用して、**NCLOB**&#x200B;および&#x200B;**NVARCHAR**&#x200B;タイプのフィールドを使用できます。
   > 
   >このオプションを選択しない場合、Oracle・データベースの文字セット（文字セット）で、すべての言語でデータ・ストレージを有効にする必要があります(AL32UTF8をお勧めします)。

* データベースのタイムゾーンを選択し、UTCで表示するかどうかを指定します（使用可能な場合）。

   詳しくは、[タイムゾーン管理](../../installation/using/time-zone-management.md)を参照してください。

### 手順4 - {#step-4---packages-to-install}をインストールするパッケージ

インストールするパッケージを選択します。

ライセンス契約を参照して、「インタラクション」や「ソーシャルマーケティング」など、インストールの資格があるソリューションやオプションを確認します。

![](assets/s_ncs_install_modules.png)

### 手順5 — 作成手順{#step-5---creation-steps}

**[!UICONTROL 作成ステップ]**&#x200B;ウィンドウでは、テーブルの作成に使用するSQLスクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle（Microsoft SQL ServerまたはPostgreSQLデータベース）の場合、管理者は、データベースオブジェクトを作成する際に使用する&#x200B;**ストレージパラメーター**&#x200B;を定義することもできます。

   これらのパラメータは、正確な表領域名を受け取ります(警告：大文字と小文字が区別されます)。 それぞれ、次のオプションの&#x200B;**[!UICONTROL 管理/プラットフォーム/オプション]**&#x200B;ノードに格納されます（[この節](../../installation/using/configuring-campaign-options.md#database)を参照）。

   * **WdbcOptions_TableSpaceUser**:スキーマに基づくユーザーテーブル
   * **WdbcOptions_TableSpaceIndex**:スキーマに基づくユーザーテーブルのインデックス
   * **WdbcOptions_TableSpaceWork**:スキーマのない作業用テーブル
   * **WdbcOptions_TableSpaceWorkIndex**:スキーマのない作業用テーブルのインデックス

* oracleデータベースの場合、Adobe CampaignユーザーはOracleライブラリにアクセスできる必要があります。通常は、**oinstall**&#x200B;グループのメンバーです。
* 「**[!UICONTROL 管理者パスワードを設定または変更]**」オプションを使用すると、Adobe Campaignオペレーターに関連付けられたパスワードを管理者権限で入力できます。

   セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順6 — データベースの作成{#step-6---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 「**[!UICONTROL 開始]**」をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースを作成したら、再接続してインスタンス設定をファイナライズできます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリにあるファイル&#x200B;**`/conf/config-<instance>.xml`**&#x200B;に保存されます。

base61データベース上のMicrosoft SQL Server設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

## 例2:既存のデータベース{#case-2--using-an-existing-database}の使用

データベースおよびユーザーは、データベース管理者によって作成され、アクセス権が正しく設定されている必要があります。

例えば、Oracle・データベースの場合、最低限必要な権限は次のとおりです。CONNECT、リソース、無制限の表領域を付与します。

既存のデータベースを使用する場合の設定手順は次のとおりです。

* [手順1 — データベースエンジンの選択](#step-1---choosing-the-database-engine),
* [手順2 — データベース接続の設定](#step-2---database-connection-settings),
* [手順3 — インストールするパッケージ](#step-3---packages-to-install),
* [手順4 — 作成ステップ](#step-4---creation-steps)、
* [手順5 — データベースの作成](#step-5---creating-the-database)を参照してください。

### 手順1 — データベースエンジンの選択{#step-1---choosing-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サーバーを特定し、実行する操作のタイプを選択します。 この場合、**[!UICONTROL 既存のデータベース]**&#x200B;を使用します。

![](assets/s_ncs_install_db_oracle_exists_01.png)

選択したデータベースエンジンに応じて、サーバ識別情報が異なる場合があります。

* **Oracle**&#x200B;エンジンの場合は、アプリケーションサーバー用に定義された&#x200B;**TNS名**&#x200B;を設定します。
* **PostgreSQL**&#x200B;または&#x200B;**DB2**&#x200B;エンジンの場合、データベースサーバーにアクセスするには、アプリケーションサーバーで定義されたDNS名（またはIPアドレス）を指定する必要があります。
* **Microsoft SQL Server**&#x200B;エンジンの場合は、次を定義する必要があります。

   1. データベース・サーバにアクセスするためにアプリケーション・サーバで定義されているDNS名（またはIPアドレス）
   1. Microsoft SQL Serverへのアクセスに使用するセキュリティメソッド：**[!UICONTROL SQL Server認証]**&#x200B;または&#x200B;**[!UICONTROL Windows NT認証]**。

      ![](assets/s_ncs_install_db_mssql_exists_01.png)

### 手順2 — データベース接続設定{#step-2---database-connection-settings}

**[!UICONTROL データベース]**&#x200B;ウィンドウで、データベース接続設定を定義します。

![](assets/s_ncs_install_db_oracle_exists_02.png)

次の設定を定義する必要があります。

* 使用するデータベースの名前を入力します。
* このデータベースに関連付けられているアカウントの名前とパスワードを入力します。

   >[!NOTE]
   >
   >スキーマ名とユーザー名の両方が一致していることを確認します。 データベースを作成する場合は、キャンペーンコンソールクライアントを使用することをお勧めします。
   >oracle・データベースの場合、アカウント名を入力する必要はありません。

* データベースがUnicodeである必要があるかどうかを示します。

### 手順3 - {#step-3---packages-to-install}をインストールするパッケージ

インストールするパッケージを選択します。

「インタラクション」や「リード」など、インストールの権利があるソリューションやオプションを確認するには、ライセンス契約を参照してください。

![](assets/s_ncs_install_modules.png)

### 手順4 — 作成手順{#step-4---creation-steps}

**[!UICONTROL 作成ステップ]**&#x200B;ウィンドウでは、テーブルの作成に使用するSQLスクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL ServerまたはPostgreSQLデータベースの場合、管理者は、データベースオブジェクトを作成する際に使用する&#x200B;**ストレージパラメーター**&#x200B;を定義できます。
* oracleデータベースの場合、Adobe CampaignユーザーはOracleライブラリにアクセスできる必要があります。通常は、**oinstall**&#x200B;グループのメンバーです。
* 「**[!UICONTROL 管理者パスワードを設定または変更]**」オプションを使用すると、Adobe Campaignオペレーターに関連付けられたパスワードを管理者権限で入力できます。

   セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順5 — データベースの作成{#step-5---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 「**[!UICONTROL 開始]**」をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースの作成が完了したら、再接続してインスタンス設定をファイナライズできます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリにあるファイル&#x200B;**`/conf/config-<instance>.xml`**&#x200B;に保存されます。

base61データベース上のMicrosoft SQL Server設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```
