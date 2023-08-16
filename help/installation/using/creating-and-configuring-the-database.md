---
product: campaign
title: データベースの作成と設定
description: データベースの作成と設定
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f40bab8c-5064-40d9-beed-101a9f22c094
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 3%

---

# データベースの作成と設定{#creating-and-configuring-the-database}

データベースを作成する場合、Adobe Campaignには次の 2 つの異なるオプションが用意されています。

1. データベースの作成またはリサイクル：新しいデータベースを作成する場合や、既存のデータベースを再利用する場合は、このオプションを選択します。 参照： [ケース 1：データベースの作成/リサイクル](#case-1--creating-recycling-a-database).
1. 既存のデータベースの使用：管理者が空のデータベースを作成済みで、そのデータベースを使用する場合、または既存のデータベースの構造を拡張する場合は、このオプションを選択します。 参照： [ケース 2：既存のデータベースの使用](#case-2--using-an-existing-database).

設定手順は以下で説明します。

>[!CAUTION]
>
>データベース、ユーザー、スキーマの名前は、数字で始めたり、特殊文字を含めたりすることはできません。
>
>次の項目のみ **内部** 識別子は、これらの操作を実行できます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## ケース 1：データベースの作成/リサイクル {#case-1--creating-recycling-a-database}

データベースを作成する手順、または既存のベースを再利用する手順を次に示します。 一部の設定は、使用するデータベースエンジンによって異なります。

次の手順が関連します。

* [手順 1 — データベースエンジンの選択](#step-1---selecting-the-database-engine),
* [手順 2 — サーバーへの接続](#step-2---connecting-to-the-server),
* [手順 3 — データベースの接続と特性](#step-3---connection-and-characteristics-of-the-database),
* [手順 4 — インストールするパッケージ](#step-4---packages-to-install),
* [手順 5 — 作成手順](#step-5---creation-steps),
* [手順 6 — データベースの作成](#step-6---creating-the-database).

### 手順 1 — データベースエンジンの選択 {#step-1---selecting-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サポートされるデータベースは Campaign に一覧表示されます [互換性マトリックス](../../rn/using/compatibility-matrix.md).

サーバーを特定し、実行する操作の種類を選択します。 この場合、 **[!UICONTROL データベースの作成またはリサイクル]**.

![](assets/s_ncs_install_db_oracle_creation01.png)

選択したデータベースエンジンに応じて、サーバーの識別情報が異なる場合があります。

* の **Oracle** エンジン、 **TNS 名** アプリケーションサーバー用に定義されます。
* の **PostgreSQL** または **DB2** エンジンでは、データベースサーバーにアクセスするには、アプリケーションサーバーで定義された DNS 名（または IP アドレス）を指定する必要があります。
* の **Microsoft SQL Server** エンジン、次を定義する必要があります。データベース・サーバにアクセスするには、アプリケーション・サーバで定義された DNS 名（または IP アドレス）を定義します。 **DNS** または **DNS`\<instance>`** （インスタンスモード）、

  >[!CAUTION]
  >
  > 20.3 以降、Windows NT 認証は廃止されます。 **[!UICONTROL SQL Server 認証]** は、Microsoft SQL Server で使用できる唯一の認証モードになりました。 [詳細情報](../../rn/using/deprecated-features.md)

  ![](assets/s_ncs_install_db_mssql_creation01.png)

### 手順 2 — サーバーへの接続 {#step-2---connecting-to-the-server}

Adobe Analytics の **[!UICONTROL サーバーアクセス]** ウィンドウで、データベース・サーバ・アクセスを定義します。

![](assets/s_ncs_install_db_oracle_creation02.png)

これをおこなうには、 **管理システムアカウント** データベースにアクセスする権限を持つ次のようになります。

* **システム** oracle・データベース
* **sa** (Microsoft SQL Server データベースの場合 )
* **postgres** （PostgreSQL データベースの場合）
* **db2inst1** DB2 データベースの場合。

### 手順 3 — データベースの接続と特性 {#step-3---connection-and-characteristics-of-the-database}

次の手順では、データベースにログオンするための設定を構成できます。

![](assets/s_ncs_install_db_oracle_creation03.png)

次の設定を定義する必要があります。

* 作成するデータベースの名前を指定します。

  >[!NOTE]
  >
  >DB2 データベースの場合、データベースの名前は 8 文字以内にする必要があります。

* このデータベースにリンクされているアカウントのパスワードを入力します。
* データベースが Unicode である必要があるかどうかを示します。

  The **[!UICONTROL Unicode データベース]** 「 」オプションを使用すると、言語に関係なく、すべての文字タイプを Unicode で保存できます。

  >[!NOTE]
  >
  >oracle・データベースの場合、 **[!UICONTROL Unicode ストレージ]** オプションを使用すると、 **NCLOB** および **NVARCHAR** フィールドを入力します。
  > 
  >このオプションを選択しない場合、Oracleデータベースの文字セット (charset) は、すべての言語でデータストレージを有効にする必要があります (AL32UTF8 をお勧めします )。

* データベースのタイムゾーンを選択し、UTC で表示するかどうかを指定します（使用可能な場合）。

  詳しくは、 [タイムゾーン管理](../../installation/using/time-zone-management.md).

### 手順 4 — インストールするパッケージ {#step-4---packages-to-install}

インストールするパッケージを選択します。

ライセンス契約を参照して、「インタラクション」や「ソーシャルマーケティング」など、インストールの資格があるソリューションやオプションを確認します。

![](assets/s_ncs_install_modules.png)

### 手順 5 — 作成手順 {#step-5---creation-steps}

The **[!UICONTROL 作成ステップ]** ウィンドウでは、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は **ストレージパラメーター** データベースオブジェクトを作成する際に使用します。

  これらのパラメータは、正確なテーブル領域名を受け取ります（警告：大文字と小文字を区別）。 それぞれ、 **[!UICONTROL 管理/プラットフォーム/オプション]** ノードを次のオプションに設定します ( [この節](../../installation/using/configuring-campaign-options.md#database)):

   * **WdbcOptions_TableSpaceUser**：スキーマに基づくユーザーテーブル
   * **WdbcOptions_TableSpaceIndex**：スキーマに基づくユーザーテーブルのインデックス
   * **WdbcOptions_TableSpaceWork**：スキーマのない作業用テーブル
   * **WdbcOptions_TableSpaceWorkIndex**：スキーマのない作業用テーブルのインデックス

* oracleデータベースの場合、Adobe Campaignユーザーは、通常、Oracleライブラリ ( **oinstall** グループ化します。
* The **[!UICONTROL 管理者パスワードを設定または変更する]** 「 」オプションを使用すると、Adobe Campaignオペレーターにリンクされているパスワードを管理者権限で入力できます。

  セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順 6 — データベースの作成 {#step-6---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 クリック **[!UICONTROL 開始]** をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースを作成したら、再接続してインスタンス設定をファイナライズできます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 参照： [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

インスタンスにリンクされたデータベースの接続設定は、ファイルに保存されます。 **`/conf/config-<instance>.xml`** は、Adobe Campaignインストールディレクトリにあります。

base61 データベース上のMicrosoft SQL Server の設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている場合の例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

## ケース 2：既存のデータベースの使用 {#case-2--using-an-existing-database}

データベースおよびユーザーは、データベース管理者によって作成され、アクセス権が正しく設定されている必要があります。

たとえば、Oracle・データベースの場合、必要な最小の権限は、GRANTCONNECT、RESOURCE および UNLIMITED TABLESPACE です。

既存のデータベースを使用する場合の設定手順は次のとおりです。

* [手順 1 — データベースエンジンの選択](#step-1---choosing-the-database-engine),
* [手順 2 — データベース接続の設定](#step-2---database-connection-settings),
* [手順 3 — インストールするパッケージ](#step-3---packages-to-install),
* [手順 4 — 作成手順](#step-4---creation-steps),
* [手順 5 — データベースの作成](#step-5---creating-the-database).

### 手順 1 — データベースエンジンの選択 {#step-1---choosing-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サーバーを特定し、実行する操作のタイプを選択します。 この場合、 **[!UICONTROL 既存のデータベースを使用]**.

![](assets/s_ncs_install_db_oracle_exists_01.png)

選択したデータベースエンジンに応じて、サーバーの識別情報が異なる場合があります。

* の **Oracle** エンジン、 **TNS 名** アプリケーションサーバー用に定義されます。
* の **PostgreSQL** または **DB2** エンジンでは、データベースサーバーにアクセスするには、アプリケーションサーバーで定義された DNS 名（または IP アドレス）を指定する必要があります。
* の **Microsoft SQL Server** エンジンは、次を定義する必要があります。

   1. データベース・サーバにアクセスするためにアプリケーション・サーバで定義された DNS 名（または IP アドレス）
   1. Microsoft SQL Server へのアクセスに使用するセキュリティメソッド： **[!UICONTROL SQL Server 認証]** または **[!UICONTROL Windows NT 認証]**.

      ![](assets/s_ncs_install_db_mssql_exists_01.png)

### 手順 2 — データベース接続の設定 {#step-2---database-connection-settings}

Adobe Analytics の **[!UICONTROL データベース]** ウィンドウで、データベース接続設定を定義します。

![](assets/s_ncs_install_db_oracle_exists_02.png)

次の設定を定義する必要があります。

* 使用するデータベースの名前を入力します。
* このデータベースに関連付けられたアカウントの名前とパスワードを入力します。

  >[!NOTE]
  >
  >スキーマ名とユーザー名の両方が一致していることを確認します。 データベースを作成する場合は、Campaign コンソールクライアントを使用することをお勧めします。
  >oracle・データベースの場合は、アカウント名を入力する必要はありません。

* データベースが Unicode である必要があるかどうかを示します。

### 手順 3 — インストールするパッケージ {#step-3---packages-to-install}

インストールするパッケージを選択します。

「インタラクション」や「リード」など、インストールの資格があるソリューションやオプションを確認するには、ライセンス契約を参照してください。

![](assets/s_ncs_install_modules.png)

### 手順 4 — 作成手順 {#step-4---creation-steps}

The **[!UICONTROL 作成ステップ]** ウィンドウでは、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は **ストレージパラメーター** データベースオブジェクトを作成する際に使用します。
* oracleデータベースの場合、Adobe Campaignユーザーは、通常、Oracleライブラリ ( **oinstall** グループ化します。
* The **[!UICONTROL 管理者パスワードを設定または変更する]** 「 」オプションを使用すると、Adobe Campaignオペレーターにリンクされているパスワードを管理者権限で入力できます。

  セキュリティ上の理由から、Adobe Campaignアカウント管理者のパスワードを定義することをお勧めします。

### 手順 5 — データベースの作成 {#step-5---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 クリック **[!UICONTROL 開始]** をクリックして確定します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースの作成が完了したら、再接続してインスタンス設定を最終決定できます。

次に、デプロイウィザードを起動して、インスタンスの設定を完了する必要があります。 参照： [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

インスタンスにリンクされたデータベースの接続設定は、ファイルに保存されます。 **`/conf/config-<instance>.xml`** は、Adobe Campaignインストールディレクトリにあります。

base61 データベース上のMicrosoft SQL Server の設定で、暗号化されたパスワードを使用して「campaign」アカウントにリンクされている場合の例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```
