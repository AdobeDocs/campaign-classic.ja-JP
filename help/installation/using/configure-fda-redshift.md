---
product: campaign
title: Amazon Redshift へのアクセスの設定
description: FDA でAmazon Redshift へのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: connectors
source-git-commit: 6939307c0b33ff662fe4ef9ae0192ae7b500a95c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 28%

---

# Amazon Redshift へのアクセスの設定 {#configure-access-to-redshift}

キャンペーンを使用 **Federated Data Access** (FDA) 外部データベースに保存されている情報を処理するオプション。 次の手順に従って、Amazon Redshift へのアクセスを設定します。

1. 設定 [Amazon Redshift データベース](#configuring-redshift)
1. Amazon Redshift の設定 [外部アカウント](#redshift-external) Campaign 内

## Linux 上のAmazon Redshift {#redshift-linux}

を設定するには、以下を実行します。 [!DNL Amazon Redshift] Linux の場合は、次の手順に従います。

1. ODBC をインストールする前に、次のパッケージが Linux ディストリビューションにインストールされていることを確認します。

   * Red Hat/CentOS の場合：

     ```
      yum update
      yum upgrade
      yum install -y grep sed tar wget perl curl
     ```

   * Debian の場合：

     ```
      apt-get update
      apt-get upgrade
      apt-get install -y grep sed tar wget perl curl
     ```

1. スクリプトを実行する前に、 `--help` オプション：

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts/
   ./redshift_odbc-setup.sh --help
   ```

1. スクリプトが存在するディレクトリにアクセスし、次のスクリプトを root ユーザーとして実行します。

   ```
     cd /usr/local/neolane/nl6/bin/fda-setup-scripts
     ./redshift_odbc-setup.sh
   ```

1. ODBC ドライバーをインストールした後、Campaign Classicを再起動する必要があります。 これをおこなうには、次のコマンドを実行します。

   ```
   systemctl stop nlserver.service
   systemctl start nlserver.service
   ```

1. Campaign では、 [!DNL Amazon Redshift] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#redshift-external).

## Amazon Redshift 外部アカウント {#redshift-external}

The [!DNL Amazon Redshift] 外部アカウントを使用すれば、Campaign インスタンスをAmazon Redshift 外部データベースに接続することができます。

1. Campaign Classic で、[!DNL Amazon Redshift] 外部アカウントを設定します。**[!UICONTROL エクスプローラー]**&#x200B;で、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. を設定します。 **[!UICONTROL Amazon Redshift]** 外部アカウントで、次を指定する必要があります。

   * **[!UICONTROL タイプ]**: Amazon Redshift

   * **[!UICONTROL サーバー]**：DNS の名前

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：DSN で指定されていない場合のデータベースの名前。DSN で指定した場合は、空のままにできます

   * **[!UICONTROL 作業スキーマ]**：作業中のスキーマの名前。 [詳細情報](https://docs.aws.amazon.com/redshift/latest/dg/r_Schemas_and_tables.html)

   * **[!UICONTROL タイムゾーン]**：サーバーのタイムゾーン

   ![](assets/amazon_redshift.png)

1. 「**[!UICONTROL 保存]**」をクリックします。
