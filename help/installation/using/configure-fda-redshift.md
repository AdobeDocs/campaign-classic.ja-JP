---
product: campaign
title: Amazon Redshift へのアクセスの設定
description: FDA でAmazon Redshift へのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: ef2b98bd-441e-4e59-bb41-4e835e250663
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 27%

---

# Amazon Redshift へのアクセスの設定 {#configure-access-to-redshift}

Campaign の使用 **連合データアクセス** （FDA）外部データベースに保存された情報を処理するオプション。 Amazon Redshift へのアクセスを設定するには、次の手順に従います。

1. 設定 [Amazon Redshift データベース](#configuring-redshift)
1. Amazon Redshift の設定 [外部アカウント](#redshift-external) Campaign 内

## Linux のAmazon Redshift {#redshift-linux}

を設定 [!DNL Amazon Redshift] linux の場合は、次の手順に従います。

1. ODBC をインストールする前に、Linux ディストリビューションに次のパッケージがインストールされていることを確認します。

   * Red Hat/CentOS:

     ```
      yum update
      yum upgrade
      yum install -y grep sed tar wget perl curl
     ```

   * Debian の場合

     ```
      apt-get update
      apt-get upgrade
      apt-get install -y grep sed tar wget perl curl
     ```

1. スクリプトを実行する前に、を使用して詳細情報にアクセスできます `--help` オプション：

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts/
   ./redshift_odbc-setup.sh --help
   ```

1. スクリプトがあるディレクトリにアクセスし、ルートユーザーとして次のスクリプトを実行します。

   ```
     cd /usr/local/neolane/nl6/bin/fda-setup-scripts
     ./redshift_odbc-setup.sh
   ```

1. ODBC ドライバをインストールしたら、Campaign Classicを再起動する必要があります。 これをおこなうには、次のコマンドを実行します。

   ```
   systemctl stop nlserver.service
   systemctl start nlserver.service
   ```

1. Campaign では、次の項目を設定できます [!DNL Amazon Redshift] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#redshift-external).

## Amazon Redshift 外部アカウント {#redshift-external}

この [!DNL Amazon Redshift] 外部アカウントを使用すると、Campaign インスタンスをAmazon Redshift 外部データベースに接続できます。

1. Campaign Classic で、[!DNL Amazon Redshift] 外部アカウントを設定します。**[!UICONTROL エクスプローラー]**&#x200B;で、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. の設定 **[!UICONTROL Amazon Redshift]** 外部アカウント。次を指定する必要があります。

   * **[!UICONTROL タイプ]**:Amazon Redshift

   * **[!UICONTROL サーバー]**：DNS の名前

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：DSN で指定されていない場合のデータベースの名前。DSN で指定した場合は、空のままにできます

   * **[!UICONTROL 作業スキーマ]**：作業用スキーマの名前。 [詳細情報](https://docs.aws.amazon.com/redshift/latest/dg/r_Schemas_and_tables.html)

   * **[!UICONTROL タイムゾーン]**：サーバーのタイムゾーン

   ![](assets/amazon_redshift.png)

1. 「**[!UICONTROL 保存]**」をクリックします。
