---
product: campaign
title: データベースの作成と設定
description: データベースの作成と設定
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f40bab8c-5064-40d9-beed-101a9f22c094
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---

# データベースの作成と設定{#creating-and-configuring-the-database}

![](../../assets/v7-only.svg)

データベースを作成する場合、Adobe Campaignには次の 2 つの異なるオプションが用意されています。

1. データベースの作成または再利用：新しいデータベースを作成する場合や、既存のデータベースを再利用する場合は、このオプションを選択します。 [ ケース 1 を参照：データベース ](#case-1--creating-recycling-a-database) を作成/リサイクルします。
1. 既存のデータベースの使用：管理者が空のデータベースを作成済みで、それを使用する場合は、このオプションを選択します。または既存のデータベースの構造を拡張する場合。 [ ケース 2 を参照：既存のデータベース ](#case-2--using-an-existing-database) を使用します。

設定手順は以下で説明します。

>[!CAUTION]
>
>データベース、ユーザー、スキーマの名前は、数字で始めたり、特殊文字を含めたりすることはできません。
>
>これらの操作を実行できるのは、**内部** 識別子だけです。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## 例 1:データベースの作成と再利用 {#case-1--creating-recycling-a-database}

データベースの作成または既存のベースの再利用の手順を次に示します。 一部の設定は、使用するデータベースエンジンによって異なります。

次の手順が関係します。

* [手順 1 — データベースエンジンの選択](#step-1---selecting-the-database-engine),
* [手順 2 — サーバーへの接続](#step-2---connecting-to-the-server),
* [手順 3 — データベースの接続と特性](#step-3---connection-and-characteristics-of-the-database),
* [手順 4 — インストールするパッケージ](#step-4---packages-to-install),
* [手順 5 — 作成ステップ](#step-5---creation-steps),
* [手順 6 — データベースの作成](#step-6---creating-the-database)を参照してください。

### 手順 1 — データベースエンジンの選択 {#step-1---selecting-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サポートされるデータベースは、Campaign の [ 互換性マトリックス ](../../rn/using/compatibility-matrix.md) に記載されています。

サーバーを特定し、実行する操作のタイプを選択します。 この場合、**[!UICONTROL データベースを作成またはリサイクル]** します。

![](assets/s_ncs_install_db_oracle_creation01.png)

選択したデータベースエンジンに応じて、サーバの識別情報が異なる場合があります。

* **Oracle** エンジンの場合は、アプリケーションサーバー用に定義された **TNS 名** を設定します。
* **PostgreSQL** または **DB2** エンジンの場合、データベースサーバーにアクセスするには、アプリケーションサーバーで定義された DNS 名（または IP アドレス）を指定する必要があります。
* **Microsoft SQL Server** エンジンの場合は、次を定義する必要があります。データベース・サーバにアクセスするためにアプリケーション・サーバで定義された DNS 名（または IP アドレス）:**DNS** または **DNS`\<instance>`**（インスタンスモード）

   >[!CAUTION]
   >
   > 20.3 以降、Windows NT 認証は廃止されます。 **[!UICONTROL SQL Server 認証]** は、Microsoft SQL Server で使用できる唯一の認証モードになりました。[詳細情報](../../rn/using/deprecated-features.md)

   ![](assets/s_ncs_install_db_mssql_creation01.png)

### 手順 2 — サーバーへの接続 {#step-2---connecting-to-the-server}

**[!UICONTROL サーバーアクセス]** ウィンドウで、データベースサーバーアクセスを定義します。

![](assets/s_ncs_install_db_oracle_creation02.png)

これをおこなうには、データベースにアクセスする権限を持つ **管理システム・アカウント** の名前とパスワードを入力します。例：

* **** oracle・データベースのシステム
* **** Microsoft SQL Server データベースの場合
* **** PostgreSQL データベースの postgres
* **db2inst1** （DB2 データベース用）

### 手順 3 — データベースの接続と特性 {#step-3---connection-and-characteristics-of-the-database}

次の手順では、データベースにログオンするための設定を指定できます。

![](assets/s_ncs_install_db_oracle_creation03.png)

次の設定を定義する必要があります。

* 作成するデータベースの名前を指定します。

   >[!NOTE]
   >
   >DB2 データベースの場合、データベースの名前は 8 文字以下にする必要があります。

* このデータベースにリンクされているアカウントのパスワードを入力します。
* データベースが Unicode である必要があるかどうかを示します。

   **[!UICONTROL Unicode データベース]** オプションを使用すると、言語に関係なく、すべての文字タイプを Unicode で保存できます。

   >[!NOTE]
   >
   >oracle・データベースでは、**[!UICONTROL Unicode ストレージ]** オプションを使用して、**NCLOB** および **NVARCHAR** タイプのフィールドを使用できます。
   > 
   >このオプションを選択しない場合、Oracle・データベースの文字セット（文字セット）ですべての言語のデータ・ストレージを有効にする必要があります (AL32UTF8 を推奨します )。

* データベースのタイムゾーンを選択し、UTC で表示するかどうかを指定します（使用可能な場合）。

   詳しくは、[ タイムゾーン管理 ](../../installation/using/time-zone-management.md) を参照してください。

### 手順 4 — インストールするパッケージ {#step-4---packages-to-install}

インストールするパッケージを選択します。

「インタラクション」や「ソーシャルマーケティング」など、インストールの資格があるソリューションやオプションを確認するには、使用許諾契約を参照してください。

![](assets/s_ncs_install_modules.png)

### 手順 5 — 作成ステップ {#step-5---creation-steps}

「**[!UICONTROL 作成ステップ]**」ウィンドウでは、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は、データベースオブジェクトの作成時に使用する **ストレージパラメータ** を定義することもできます。

   これらのパラメータは、正確な表領域名を受け取ります ( 警告：大文字と小文字が区別されます )。 それぞれ、次のオプションの **[!UICONTROL 管理/プラットフォーム/オプション]** ノードに格納されます（[ この節 ](../../installation/using/configuring-campaign-options.md#database) を参照）。

   * **WdbcOptions_TableSpaceUser**:スキーマに基づくユーザーテーブル
   * **WdbcOptions_TableSpaceIndex**:スキーマに基づくユーザーテーブルのインデックス
   * **WdbcOptions_TableSpaceWork**:スキーマのない作業用テーブル
   * **WdbcOptions_TableSpaceWorkIndex**:スキーマのない作業用テーブルのインデックス

* oracleデータベースの場合、Adobe CampaignユーザーはOracleライブラリにアクセスできる必要があります。通常は、**oinstall** グループのメンバーです。
* 「**[!UICONTROL 管理者パスワードを設定または変更]**」オプションを使用すると、Adobe Campaignオペレーターに関連するパスワードを管理者権限で入力できます。

   セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順 6 — データベースの作成 {#step-6---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 「**[!UICONTROL 開始]**」をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースを作成したら、再接続してインスタンス設定をファイナライズできます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 [ デプロイウィザード ](../../installation/using/deploying-an-instance.md#deployment-wizard) を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリにあるファイル **`/conf/config-<instance>.xml`** に保存されます。

base61 データベース上のMicrosoft SQL Server 設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

## 例 2:既存のデータベースの使用 {#case-2--using-an-existing-database}

データベースおよびユーザーは、データベース管理者によって作成され、アクセス権が正しく設定されている必要があります。

例えば、Oracle・データベースの場合、最低限必要な権限は次のとおりです。CONNECT、リソース、および無制限の表領域を付与します。

既存のデータベースを使用する場合の設定手順は次のとおりです。

* [手順 1 — データベースエンジンの選択](#step-1---choosing-the-database-engine),
* [手順 2 — データベース接続の設定](#step-2---database-connection-settings),
* [手順 3 — インストールするパッケージ](#step-3---packages-to-install),
* [手順 4 — 作成ステップ](#step-4---creation-steps),
* [手順 5 — データベースの作成](#step-5---creating-the-database)を参照してください。

### 手順 1 — データベースエンジンの選択 {#step-1---choosing-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サーバーを特定し、実行する操作のタイプを選択します。 この場合、**[!UICONTROL 既存のデータベース]** を使用します。

![](assets/s_ncs_install_db_oracle_exists_01.png)

選択したデータベースエンジンに応じて、サーバの識別情報が異なる場合があります。

* **Oracle** エンジンの場合は、アプリケーションサーバー用に定義された **TNS 名** を設定します。
* **PostgreSQL** または **DB2** エンジンの場合、データベースサーバーにアクセスするには、アプリケーションサーバーで定義された DNS 名（または IP アドレス）を指定する必要があります。
* **Microsoft SQL Server** エンジンの場合は、次を定義する必要があります。

   1. データベース・サーバにアクセスするためにアプリケーション・サーバで定義された DNS 名（または IP アドレス）
   1. Microsoft SQL Server へのアクセスに使用するセキュリティメソッド：**[!UICONTROL SQL Server 認証]** または **[!UICONTROL Windows NT 認証]**。

      ![](assets/s_ncs_install_db_mssql_exists_01.png)

### 手順 2 — データベース接続の設定 {#step-2---database-connection-settings}

**[!UICONTROL データベース]** ウィンドウで、データベース接続設定を定義します。

![](assets/s_ncs_install_db_oracle_exists_02.png)

次の設定を定義する必要があります。

* 使用するデータベースの名前を入力します。
* このデータベースに関連付けられたアカウントの名前とパスワードを入力します。

   >[!NOTE]
   >
   >スキーマ名とユーザー名の両方が一致していることを確認します。 データベースを作成する場合は、Campaign コンソールクライアントを使用することをお勧めします。
   >oracle・データベースの場合、アカウント名を入力する必要はありません。

* データベースが Unicode である必要があるかどうかを示します。

### 手順 3 — インストールするパッケージ {#step-3---packages-to-install}

インストールするパッケージを選択します。

「インタラクション」や「リード」など、インストールの権利があるソリューションやオプションを確認するには、ライセンス契約を参照してください。

![](assets/s_ncs_install_modules.png)

### 手順 4 — 作成ステップ {#step-4---creation-steps}

「**[!UICONTROL 作成ステップ]**」ウィンドウでは、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は、データベースオブジェクトの作成時に使用する **ストレージパラメータ** を定義できます。
* oracleデータベースの場合、Adobe CampaignユーザーはOracleライブラリにアクセスできる必要があります。通常は、**oinstall** グループのメンバーです。
* 「**[!UICONTROL 管理者パスワードを設定または変更]**」オプションを使用すると、Adobe Campaignオペレーターに関連するパスワードを管理者権限で入力できます。

   セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順 5 — データベースの作成 {#step-5---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 「**[!UICONTROL 開始]**」をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースの作成が完了したら、再接続してインスタンス設定をファイナライズできます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 [ デプロイウィザード ](../../installation/using/deploying-an-instance.md#deployment-wizard) を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリにあるファイル **`/conf/config-<instance>.xml`** に保存されます。

base61 データベース上のMicrosoft SQL Server 設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```
