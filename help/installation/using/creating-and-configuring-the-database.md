---
solution: Campaign Classic
product: campaign
title: データベースの作成と設定
description: データベースの作成と設定
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---


# データベースの作成と設定{#creating-and-configuring-the-database}

データベースを作成する場合、Adobe Campaignには次の2つの異なるオプションが用意されています。

1. データベースの作成またはリサイクル：新しいデータベースを作成する場合、または既存のデータベースを再使用する場合は、このオプションを選択します。 詳しくは、 [ケース1を参照してください。データベースの作成/リサイクル](#case-1--creating-recycling-a-database)。
1. 既存のデータベースの使用：管理者が空のデータベースを既に作成済みで、それを使用する場合は、このオプションを選択します。または既存のデータベースの構造を拡張する場合。 詳しくは、 [ケース2を参照してください。既存のデータベースを使用する](#case-2--using-an-existing-database)。

設定手順の詳細は以下のとおりです。

>[!CAUTION]
>
>データベース、ユーザー、スキーマの名前に数字を開始したり、特殊文字を含めたりすることはできません。
>
>これらの操作を実行できるのは **内部** IDのみです。 For more on this, refer to [Internal identifier](../../installation/using/campaign-server-configuration.md#internal-identifier).

## ケース1:データベースの作成/リサイクル {#case-1--creating-recycling-a-database}

データベースを作成する手順、または既存のベースを再利用する手順を以下に示します。 設定によっては、使用するデータベースエンジンに依存するものもあります。

次の手順が関係します。

* [手順1 — データベースエンジンの選択](#step-1---selecting-the-database-engine)、
* [手順2 — サーバーへの接続](#step-2---connecting-to-the-server)、
* [手順3 — データベースの接続と特性](#step-3---connection-and-characteristics-of-the-database)、
* [手順4 — インストールするパッケージ](#step-4---packages-to-install)、
* [手順5 — 作成手順](#step-5---creation-steps)、
* [手順6 — データベースの作成](#step-6---creating-the-database)。

### 手順1 — データベースエンジンの選択 {#step-1---selecting-the-database-engine}

ドロップダウン・リストの中からデータベース・エンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サポートされるデータベースは、キャンペーン [互換表に記載されています](../../rn/using/compatibility-matrix.md)。

サーバーを識別し、実行する操作の種類を選択します。 この場合は、データベースを **[!UICONTROL 作成またはリサイクルします]**。

![](assets/s_ncs_install_db_oracle_creation01.png)

選択したデータベースエンジンによって、サーバ識別情報が異なる場合があります。

* **Oracle** ・エンジンの場合は、アプリケーション・サーバーに対して定義されている **TNS名** を入力します。
* PostgreSQL **または** DB2 **** エンジンの場合は、データベースサーバーにアクセスするために、アプリケーションサーバーで定義されているDNS名（またはIPアドレス）を指定する必要があります。
* **Microsoft SQL Server** Engineの場合は、次を定義する必要があります。データベースサーバーにアクセスするためにアプリケーションサーバーで定義されているDNS名（またはIPアドレス）。 **DNS** または **DNS`\<instance>`** （インスタンスモード）、

   >[!CAUTION]
   >
   > 20.3以降、Windows NT認証は廃止されます。 **[!UICONTROL Microsoft SQL Serverで使用できる認証モードは]** 、SQL Server認証のみです。 [詳細を表示](../../rn/using/deprecated-features.md)

   ![](assets/s_ncs_install_db_mssql_creation01.png)

### 手順2 — サーバーへの接続 {#step-2---connecting-to-the-server}

「 **[!UICONTROL サーバー・アクセス]** 」ウィンドウで、データベース・サーバー・アクセスを定義します。

![](assets/s_ncs_install_db_oracle_creation02.png)

これを行うには、データベースにアクセスする権限を持つ **管理システム・アカウントの名前とパスワードを入力します** 。例：

* **oracleデータベースのシステム** 、
* **Microsoft SQL Serverデータベース用のsa** 、
* **PostgreSQLデータベース用のpostgres** 、
* **db2inst1** （DB2データベース用）

### 手順3 — データベースの接続と特性 {#step-3---connection-and-characteristics-of-the-database}

次の手順では、データベースにログオンするための設定を指定します。

![](assets/s_ncs_install_db_oracle_creation03.png)

次の設定を定義する必要があります。

* 作成するデータベースの名前を指定します。

   >[!NOTE]
   >
   >DB2データベースの場合、データベース名は8文字以下にする必要があります。

* このデータベースにリンクされているアカウントのパスワードを入力してください。
* データベースがUnicodeである必要があるかどうかを示します。

   「 **[!UICONTROL Unicodeデータベース]** 」オプションを使用すると、言語に関係なく、すべての文字タイプをUnicodeで保存できます。

   >[!NOTE]
   >
   >oracleデータベースでは、 **[!UICONTROL Unicodeストレージ]** ・オプションを使用して、 **NCLOB** 型フィールドと **NVARCHAR** 型フィールドを使用できます。
   > 
   >このオプションを選択しない場合、Oracleデータベースの文字セット(charset)は、すべての言語でデータストレージを有効にする必要があります（AL32UTF8を推奨）。

* データベースのタイムゾーンを選択し、UTC（可能な場合）にするかどうかを指定します。

   For more on this, refer to [Time zone management](../../installation/using/time-zone-management.md).

### 手順4 — インストールするパッケージ {#step-4---packages-to-install}

インストールするパッケージを選択します。

使用許諾契約書を参照して、「インタラクション」や「ソーシャルマーケティング」など、インストールの権利があるソリューションとオプションを確認します。

![](assets/s_ncs_install_modules.png)

### 手順5 — 作成手順 {#step-5---creation-steps}

「 **[!UICONTROL 作成ステップ]** 」ウィンドウでは、テーブルの作成に使用するSQLスクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server、またはPostgreSQLデータベースの場合、管理者は、データベースオブジェクトの作成時に使用する **ストレージパラメータ** を定義することもできます。

   これらのパラメータは、正確な表領域名を受け取ります(警告：大文字と小文字が区別されます)。 これらは、それぞれ、 **[!UICONTROL 管理/プラットフォーム/オプション]** ( [この節を参照](../../installation/using/configuring-campaign-options.md#database))のノードに保存されます。

   * **WdbcOptions_TableSpaceUser**:スキーマに基づくユーザーテーブル
   * **WdbcOptions_TableSpaceIndex**:スキーマに基づくユーザーテーブルのインデックス
   * **WdbcOptions_TableSpaceWork**:スキーマのない作業テーブル
   * **WdbcOptions_TableSpaceWorkIndex**:スキーマのない作業テーブルのインデックス

* oracleデータベースの場合、Adobe Campaignユーザーは、通常、 **oinstall** グループのメンバーとして、Oracleライブラリにアクセスできる必要があります。
* 「 **[!UICONTROL Set or change the administrator password]** 」オプションを使用すると、管理者権限を持つAdobe Campaign演算子にリンクされたパスワードを入力できます。

   セキュリティを確保するために、Adobe Campaignアカウント管理者パスワードを定義することをお勧めします。

### 手順6 — データベースの作成 {#step-6---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 Click **[!UICONTROL Start]** to confirm.

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースが作成されたら、再接続してインスタンス設定を終了できます。

次に、配置ウィザードを開始して、インスタンスの設定を完了する必要があります。 「 [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)」を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリに **`/conf/config-<instance>.xml`** あるファイルに保存されます。

base61データベース上のMicrosoft SQL Server設定の例で、暗号化されたパスワードを使用して&#39;キャンペーン&#39;アカウントにリンクされています。

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

## ケース2:既存のデータベースの使用 {#case-2--using-an-existing-database}

データベースおよびユーザーは、データベース管理者が作成したデータベースであり、アクセス権が正しく設定されている必要があります。

たとえば、Oracle・データベースの場合、必要な最小限の権限は次のとおりです。CONNECT、リソース、および無制限の表領域を付与します。

既存のデータベースを使用する場合の設定手順は次のとおりです。

* [手順1 — データベースエンジンの選択](#step-1---choosing-the-database-engine)、
* [手順2 — データベース接続の設定](#step-2---database-connection-settings)、
* [手順3 — インストールするパッケージ](#step-3---packages-to-install)、
* [手順4 — 作成手順](#step-4---creation-steps)、
* [手順5 — データベースの作成](#step-5---creating-the-database)。

### 手順1 — データベースエンジンの選択 {#step-1---choosing-the-database-engine}

ドロップダウン・リストからデータベース・エンジンを選択します。

![](assets/s_ncs_install_db_select_engine.png)

サーバーを特定し、実行する操作の種類を選択します。 この場合、既存のデータベース **[!UICONTROL を使用し]**&#x200B;ます。

![](assets/s_ncs_install_db_oracle_exists_01.png)

選択したデータベースエンジンによって、サーバ識別情報が異なる場合があります。

* **Oracle** ・エンジンの場合は、アプリケーション・サーバーに対して定義されている **TNS名** を入力します。
* PostgreSQL **または** DB2 **** エンジンの場合は、データベースサーバーにアクセスするために、アプリケーションサーバーで定義されているDNS名（またはIPアドレス）を指定する必要があります。
* **Microsoft SQL Server** Engineの場合は、次を定義する必要があります。

   1. データベースサーバーにアクセスするためにアプリケーションサーバーで定義されているDNS名（またはIPアドレス）、
   1. microsoft SQL Serverにアクセスするためのセキュリティメソッド： **[!UICONTROL SQL Server認証]** 、 **[!UICONTROL Windows NT認証]**。

      ![](assets/s_ncs_install_db_mssql_exists_01.png)

### 手順2 — データベース接続の設定 {#step-2---database-connection-settings}

「 **[!UICONTROL Database]** 」ウィンドウで、データベース接続の設定を定義します。

![](assets/s_ncs_install_db_oracle_exists_02.png)

次の設定を定義する必要があります。

* 使用するデータベースの名前を入力します。
* このデータベースに関連付けられたアカウントの名前とパスワードを入力します。

   >[!NOTE]
   >
   >スキーマ名とユーザー名の両方が一致していることを確認します。 データベースを作成する場合、キャンペーンコンソールクライアントを使用することをお勧めします。
   >oracleデータベースの場合は、アカウント名を入力する必要はありません。

* データベースをUnicodeにするかどうかを指定します。

### 手順3 — インストールするパッケージ {#step-3---packages-to-install}

インストールするパッケージを選択します。

使用許諾契約書を参照して、「お問い合わせ」や「リード」など、インストールの権利があるソリューションとオプションを確認してください。

![](assets/s_ncs_install_modules.png)

### 手順4 — 作成手順 {#step-4---creation-steps}

「 **[!UICONTROL 作成ステップ]** 」ウィンドウでは、テーブルの作成に使用するSQLスクリプトを表示および編集できます。

![](assets/s_ncs_install_db_oracle_creation04.png)

* oracle、Microsoft SQL Server、またはPostgreSQLデータベースの場合、管理者は、データベースオブジェクトの作成時に使用する **ストレージパラメータ** を定義できます。
* oracleデータベースの場合、Adobe Campaignユーザーは、通常、 **oinstall** グループのメンバーとして、Oracleライブラリにアクセスできる必要があります。
* 「 **[!UICONTROL Set or change the administrator password]** 」オプションを使用すると、管理者権限を持つAdobe Campaign演算子にリンクされたパスワードを入力できます。

   セキュリティを確保するために、Adobe Campaignアカウント管理者パスワードを定義することをお勧めします。

### Step 5 - Creating the database {#step-5---creating-the-database}

ウィザードの最後の段階では、データベースを作成できます。 Click **[!UICONTROL Start]** to confirm.

![](assets/s_ncs_install_db_oracle_creation06.png)

データベースの作成が完了したら、再接続してインスタンス設定を確定できます。

次に、配置ウィザードを開始して、インスタンスの設定を完了する必要があります。 「 [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)」を参照してください。

インスタンスにリンクされたデータベースの接続設定は、Adobe Campaignのインストールディレクトリに **`/conf/config-<instance>.xml`** あるファイルに保存されます。

base61データベース上のMicrosoft SQL Server設定の例で、暗号化されたパスワードを使用して&#39;キャンペーン&#39;アカウントにリンクされています。

```
<dbcnx encrypted="1" login="campaign:myBase" password="myPassword" provider="DB" server="dbServer"/>
```

