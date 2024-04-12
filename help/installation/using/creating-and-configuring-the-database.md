---
product: campaign
title: データベースの作成と設定
description: データベースの作成と設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f40bab8c-5064-40d9-beed-101a9f22c094
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 1%

---

# データベースの作成と設定{#creating-and-configuring-the-database}

データベースを作成する場合、Adobe Campaignには次の 2 つの異なるオプションが用意されています。

1. データベースの作成または再利用：新しいデータベースを作成する場合や、既存のデータベースを再利用する場合は、このオプションを選択します。 こちらを参照してください [ケース 1：データベースの作成とリサイクル](#case-1--creating-recycling-a-database).
1. 既存のデータベースの使用：管理者によって空のデータベースが既に作成されていて、それを使用する場合は、このオプションを選択します。または、既存のデータベースの構造を拡張します。 こちらを参照してください [ケース 2：既存のデータベースの使用](#case-2--using-an-existing-database).

設定手順について詳しくは、以下を参照してください。

>[!CAUTION]
>
>データベース、ユーザーおよびスキーマの名前は、数字で始めたり、特殊文字を含めたりしないでください。
>
>のみ **内部** 識別子は、これらの操作を実行できます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

## ケース 1：データベースの作成とリサイクル {#case-1--creating-recycling-a-database}

データベースを作成したり、既存のベースを再利用したりする手順を以下に示します。 一部の設定は、使用するデータベースエンジンによって異なります。

関係する手順は次のとおりです。

* [手順 1 - データベースエンジンの選択](#step-1---selecting-the-database-engine),
* [手順 2 - サーバーへの接続](#step-2---connecting-to-the-server),
* [手順 3 - データベースの接続と特性](#step-3---connection-and-characteristics-of-the-database),
* [手順 4 - インストールするパッケージ](#step-4---packages-to-install),
* [手順 5 – 作成手順](#step-5---creation-steps),
* [手順 6 - データベースの作成](#step-6---creating-the-database).

### 手順 1 - データベースエンジンの選択 {#step-1---selecting-the-database-engine}

ドロップダウンリストに表示されるデータベースエンジンの中から選択します。

![](assets/s_ncs_install_db_select_engine.png)

サポートされるデータベースは Campaign に一覧表示されます [互換性マトリックス](../../rn/using/compatibility-matrix.md).

サーバーを特定し、実行する操作のタイプを選択します。 この場合、 **[!UICONTROL データベースの作成またはリサイクル]**.

![](assets/s_ncs_install_db_oracle_creation01.png)

選択したデータベースエンジンによって、サーバー識別情報が異なる場合があります。

* の場合 **Oracle** エンジン、入力 **TNS 名** アプリケーションサーバー用に定義されます。
* の場合 **PostgreSQL** または **DB2** エンジン：データベースサーバーにアクセスするには、アプリケーションサーバーで定義されている DNS 名（または IP アドレス）を指定する必要があります。
* の場合 **Microsoft SQL Server** データベースサーバーにアクセスするには、アプリケーションサーバーで定義されている DNS 名（または IP アドレス）を定義する必要があります。 **DNS** または **DNS`\<instance>`** （インスタンスモード）、

  >[!CAUTION]
  >
  > 20.3 以降、Windows NT 認証は廃止されます。 **[!UICONTROL SQL Server 認証]** は、Microsoft SQL Server で使用できる唯一の認証モードになりました。 [詳細情報](../../rn/using/deprecated-features.md)

  ![](assets/s_ncs_install_db_mssql_creation01.png)

### 手順 2 - サーバーへの接続 {#step-2---connecting-to-the-server}

が含まれる **[!UICONTROL サーバーアクセス]** ウィンドウで、データベースサーバーへのアクセスを定義します。

![](assets/s_ncs_install_db_oracle_creation02.png)

それには、ユーザーの名前とパスワードを **管理システムアカウント** データベースにアクセスする権限を持つもの。例：

* **system** oracleデータベースの場合、
* **土** Microsoft SQL Server データベースの場合、
* **postgres** PostgreSQL データベースの場合、
* **db2inst1** DB2 データベースの場合。

### 手順 3 - データベースの接続と特性 {#step-3---connection-and-characteristics-of-the-database}

次の手順では、データベースにログオンするための設定を構成します。

![](assets/s_ncs_install_db_oracle_creation03.png)

次の設定を定義する必要があります。

* 作成するデータベースの名前を指定します。

  >[!NOTE]
  >
  >DB2 データベースの場合、データベース名は 8 文字以下にする必要があります。

* このデータベースにリンクされているアカウントのパスワードを入力します。
* データベースが Unicode である必要があるかどうかを示します。

  この **[!UICONTROL Unicode データベース]** オプションを使用すると、言語に関係なく、すべての文字タイプを Unicode で保存できます。

  >[!NOTE]
  >
  >oracleデータベースを使用すると、 **[!UICONTROL Unicode ストレージ]** オプションでは、以下を使用できます **NCLOB** および **NVARCHAR** フィールドを入力します。
  > 
  >このオプションを選択しない場合、Oracleデータベースのキャラクタ・セット（文字セット）ですべての言語でのデータ・ストレージを有効にする必要があります（AL32UTF8 をお勧めします）。

* データベースのタイムゾーンを選択し、UTC （使用可能な場合）にするかどうかを指定します。

  詳しくは、次を参照してください [タイムゾーンの管理](../../installation/using/time-zone-management.md).

### 手順 4 - インストールするパッケージ {#step-4---packages-to-install}

インストールするパッケージを選択します。

ライセンス契約を参照して、「インタラクション」や「ソーシャルマーケティング」など、インストールする権利のあるソリューションとオプションを確認します。

![](assets/s_ncs_install_modules.png)

### 手順 5 – 作成手順 {#step-5---creation-steps}

この **[!UICONTROL 作成ステップ]** ウィンドウを使用すると、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は次も定義できます。 **ストレージパラメーター** データベース オブジェクトの作成時に使用されます。

  これらのパラメータは、正確な表領域名を受け取ります（警告：大文字と小文字が区別されます）。 これらはそれぞれ、 **[!UICONTROL 管理/ プラットフォーム / オプション]** 以下のオプションのノード（を参照） [この節](../../installation/using/configuring-campaign-options.md#database)）:

   * **WdbcOptions_TableSpaceUser**：スキーマに基づくユーザーテーブル
   * **WdbcOptions_TableSpaceIndex**：スキーマに基づいたユーザーテーブルのインデックス
   * **WdbcOptions_TableSpaceWork**：スキーマのない作業用テーブル
   * **WdbcOptions_TableSpaceWorkIndex**：スキーマのない作業用テーブルのインデックス

* oracleデータベースの場合、Adobe Campaign ユーザーは、通常、のメンバーとして、Oracleライブラリにアクセスできる必要があります **oinstall** グループ。
* この **[!UICONTROL 管理者パスワードの設定または変更]** 「」オプションを使用すると、管理者権限を持つAdobe Campaign オペレーターにリンクするパスワードを入力できます。

  セキュリティ保護のため、Adobe Campaign アカウント管理者のパスワードを定義することをお勧めします。

### 手順 6 - データベースの作成 {#step-6---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 クリック **[!UICONTROL 開始]** を確認します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースが作成されたら、再接続してインスタンス設定を完了できます。

インスタンスの設定を完了するには、デプロイメントウィザードを開始する必要があります。 こちらを参照してください [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

インスタンスにリンクされているデータベースの接続設定は、ファイルに保存されます **`/conf/config-<instance>.xml`** Adobe Campaignのインストールディレクトリにあります。

暗号化されたパスワードを使用して「campaign」アカウントにリンクされた base61 データベース上のMicrosoft SQL Server 設定の例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

## ケース 2：既存のデータベースの使用 {#case-2--using-an-existing-database}

データベース管理者がデータベースおよびユーザーを作成し、アクセス権が正しく設定されている必要があります。

たとえば、Oracle・データベースの場合、必要な最小権限は、GRANTCONNECT、RESOURCE および UNLIMITED TABLESPACE です。

既存のデータベースを使用するには、次の設定手順に従います。

* [手順 1 - データベースエンジンの選択](#step-1---choosing-the-database-engine),
* [手順 2 - データベース接続設定](#step-2---database-connection-settings),
* [手順 3 - インストールするパッケージ](#step-3---packages-to-install),
* [手順 4 – 作成手順](#step-4---creation-steps),
* [手順 5 - データベースの作成](#step-5---creating-the-database).

### 手順 1 - データベースエンジンの選択 {#step-1---choosing-the-database-engine}

ドロップダウンリストからデータベースエンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サーバーを特定し、実行する操作のタイプを選択します。 この場合、 **[!UICONTROL 既存のデータベースを使用]**.

![](assets/s_ncs_install_db_oracle_exists_01.png)

選択したデータベースエンジンによって、サーバー識別情報が異なる場合があります。

* の場合 **Oracle** エンジン、入力 **TNS 名** アプリケーションサーバー用に定義されます。
* の場合 **PostgreSQL** または **DB2** エンジン：データベースサーバーにアクセスするには、アプリケーションサーバーで定義されている DNS 名（または IP アドレス）を指定する必要があります。
* の場合 **Microsoft SQL Server** エンジン。次を定義する必要があります。

   1. データベースサーバーにアクセスするためにアプリケーションサーバーで定義されている DNS 名（または IP アドレス）
   1. Microsoft SQL Server へのアクセスに使用するセキュリティ方式： **[!UICONTROL SQL Server 認証]** または **[!UICONTROL Windows NT 認証]**.

      ![](assets/s_ncs_install_db_mssql_exists_01.png)

### 手順 2 - データベース接続設定 {#step-2---database-connection-settings}

が含まれる **[!UICONTROL データベース]** ウィンドウで、データベース接続設定を定義します。

![](assets/s_ncs_install_db_oracle_exists_02.png)

次の設定を定義する必要があります。

* 使用するデータベースの名前を入力します。
* このデータベースに関連付けられているアカウントの名前とパスワードを入力します。

  >[!NOTE]
  >
  >スキーマ名とユーザー名の両方が一致することを確認してください。 データベースを作成するには、Campaign コンソールクライアントを使用することをお勧めします。
  >oracle・データベースの場合は、アカウント名を入力する必要はありません。

* データベースを Unicode にするかどうかを指定します。

### 手順 3 - インストールするパッケージ {#step-3---packages-to-install}

インストールするパッケージを選択します。

ライセンス契約を参照して、「インタラクション」や「リード」など、インストールする権利のあるソリューションやオプションを確認します。

![](assets/s_ncs_install_modules.png)

### 手順 4 – 作成手順 {#step-4---creation-steps}

この **[!UICONTROL 作成ステップ]** ウィンドウを使用すると、テーブルの作成に使用する SQL スクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server または PostgreSQL データベースの場合、管理者は次を定義できます。 **ストレージパラメーター** データベース オブジェクトの作成時に使用されます。
* oracleデータベースの場合、Adobe Campaign ユーザーは、通常、のメンバーとして、Oracleライブラリにアクセスできる必要があります **oinstall** グループ。
* この **[!UICONTROL 管理者パスワードの設定または変更]** 「」オプションを使用すると、管理者権限を持つAdobe Campaign オペレーターにリンクするパスワードを入力できます。

  セキュリティ保護のため、Adobe Campaign アカウント管理者のパスワードを定義することをお勧めします。

### 手順 5 - データベースの作成 {#step-5---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 クリック **[!UICONTROL 開始]** を確認します。

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースの作成が完了したら、再接続してインスタンス設定を完了できます。

インスタンスの設定を完了するには、デプロイメントウィザードを開始する必要があります。 こちらを参照してください [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

インスタンスにリンクされているデータベースの接続設定は、ファイルに保存されます **`/conf/config-<instance>.xml`** Adobe Campaignのインストールディレクトリにあります。

暗号化されたパスワードを使用して「campaign」アカウントにリンクされた base61 データベース上のMicrosoft SQL Server 設定の例：

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```
