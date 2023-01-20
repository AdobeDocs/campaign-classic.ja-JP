---
product: campaign
title: Google BigQuery へのアクセスの設定
description: FDA でGoogle BigQuery へのアクセスを設定する方法を説明します
audience: platform
content-type: reference
topic-tags: connectors
exl-id: ebaad59f-0607-4090-92d0-e457fbf9a348
source-git-commit: 5ad84f77b0618f2e8b948a3712bc106c19b03788
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 9%

---

# Google BigQuery へのアクセスの設定 {#configure-fda-google-big-query}

![](../../assets/v7-only.svg)

Adobe Campaign Classicを使用 **Federated Data Access** (FDA) 外部データベースに保存された情報を処理するオプション。 次の手順に従って、へのアクセスを設定します。 [!DNL Google BigQuery].

1. 設定 [!DNL Google BigQuery] オン [Windows](#google-windows) または [Linux](#google-linux)
1. の設定 [!DNL Google BigQuery] [外部アカウント](#google-external) Adobe Campaign Classic
1. 設定 [!DNL Google BigQuery] コネクタの一括読み込み [Windows](#bulk-load-windows) または [Linux](#bulk-load-linux)

>[!NOTE]
>
> [!DNL Google BigQuery] コネクタは、ホスト型、ハイブリッド型、オンプレミス型のデプロイメントで使用できます。 詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Google BigQuery（Windows 上） {#google-windows}

### Windows でのドライバのセットアップ {#driver-window}

1. [Windows 用の ODBC ドライバー](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers)をダウンロードします。

1. Windows で ODBC ドライバーを設定します。 詳しくは、[このページ](https://storage.googleapis.com/simba-bq-release/jdbc/Simba%20JDBC%20Driver%20for%20Google%20BigQuery%20Install%20and%20Configuration%20Guide.pdf)を参照してください。

1. の [!DNL Google BigQuery] コネクタが機能するには、Adobe Campaign Classicが接続するには次のパラメーターが必要です。

   * **[!UICONTROL プロジェクト]**:既存のプロジェクトを作成するか、使用します。

      詳しくは、[このページ](https://cloud.google.com/resource-manager/docs/creating-managing-projects)を参照してください。

   * **[!UICONTROL サービスアカウント]**:サービスアカウントを作成します。

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-accounts)を参照してください。

   * **[!UICONTROL キーファイルのパス]**:の **[!UICONTROL サービスアカウント]** にはが必要です **[!UICONTROL キーファイル]** の [!DNL Google BigQuery] ODBC を介した接続

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)を参照してください。

   * **[!UICONTROL データセット]**: **[!UICONTROL データセット]** は、ODBC 接続の場合はオプションです。 各クエリは、テーブルの場所にあるデータセットを提供し、 **[!UICONTROL データセット]** は必須です [!DNL Google BigQuery] Adobe Campaign Classicの FDA コネクタ。

      詳しくは、[このページ](https://cloud.google.com/bigquery/docs/datasets)を参照してください。

1. Adobe Campaign Classicで、 [!DNL Google BigQuery] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#google-external).

### Windows での一括読み込みの設定 {#bulk-load-window}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 の使用をお勧めします。詳しくは、 [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じてより高速に転送できます。

1. このから Windows 64 ビット (x86_64) アーカイブをダウンロード [ページ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) 対応するディレクトリに抽出します。

1. を実行します。 `google-cloud-sdk\install.sh` スクリプト path 変数の設定を受け入れる必要があります。

1. インストール後に、パス変数を確認します。 `...\google-cloud-sdk\bin` が設定されている。 そうでない場合は、手動で追加します。

1. 内  `..\google-cloud-sdk\bin\bq.cmd` ファイルを開き、 `CLOUDSDK_PYTHON` ローカル変数を使用して、Python のインストール場所にリダイレクトされます。

   例：

   ![](assets/google-big-query_1.png)

1. Adobe Campaign Classicを再起動して、変更を反映させます。

## Google BigQuery（Linux 上） {#google-linux}

### Linux でのドライバの設定 {#driver-linux}

ドライバを設定する前に、スクリプトとコマンドを root ユーザが実行する必要があることに注意してください。 また、スクリプトの実行中にGoogle DNS 8.8.8.8 を使用することをお勧めします。

を設定するには、以下を実行します。 [!DNL Google BigQuery] Linux の場合は、次の手順に従います。

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

1. インストール前にシステムを更新する：

   * Red Hat/CentOS の場合：

      ```
      # install unixODBC driver manager
      yum install -y unixODBC
      ```

   * Debian の場合：

      ```
      # install unixODBC driver manager
      apt-get install -y odbcinst1debian2 libodbc1 odbcinst unixodbc
      ```

1. スクリプトを実行する前に、—help 引数を指定して詳細情報を取得できます。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_odbc-setup.sh --help
   ```

1. スクリプトが存在するディレクトリにアクセスし、次のスクリプトを root ユーザーとして実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_odbc-setup.sh
   ```

### Linux での一括読み込みの設定 {#bulk-load-linux}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 の使用をお勧めします。詳しくは、 [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じてより高速に転送できます。

1. ODBC をインストールする前に、次のパッケージが Linux ディストリビューションにインストールされていることを確認します。

   * Red Hat/CentOS の場合：

      ```
      yum update
      yum upgrade
      yum install -y python3
      ```

   * Debian の場合：

      ```
      apt-get update
      apt-get upgrade
      apt-get install -y python3
      ```

1. スクリプトが存在するディレクトリにアクセスし、次のスクリプトを実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_sdk-setup.sh
   ```

## Google BigQuery 外部アカウント {#google-external}

次を作成する必要があります： [!DNL Google BigQuery] Adobe Campaign Classicインスタンスを [!DNL Google BigQuery] 外部データベース。

1. Adobe Campaign Classicから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. [!DNL Google BigQuery] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Google BigQuery]

   * **[!UICONTROL サービスアカウント]**:メール **[!UICONTROL サービスアカウント]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/iam/docs/creating-managing-service-accounts).

   * **[!UICONTROL プロジェクト]**:の名前 **[!UICONTROL プロジェクト]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

   * **[!UICONTROL キーファイルのパス]**:
      * **[!UICONTROL キーファイルをサーバーにアップロード]**:選択 **[!UICONTROL ここをクリックしてアップロード]** Adobe Campaign Classicを使用してキーをアップロードする場合。

      * **[!UICONTROL 手動でキーのファイルパスを入力]**:既存のキーを使用する場合は、このフィールドに絶対パスをコピーして貼り付けます。
   * **[!UICONTROL データセット]**:の名前 **[!UICONTROL データセット]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/bigquery/docs/datasets-intro).

   ![](assets/google-big-query.png)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|:-:|:-:|
| ProxyType | ODBC および SDK コネクタを使用した BigQuery への接続に使用するプロキシのタイプ。 </br>HTTP（デフォルト）、http_no_tunnel、socks4 および socks5 が現在サポートされています。 |
| ProxyHost | プロキシに到達できるホスト名または IP アドレス。 |
| ProxyPort | プロキシが実行されているポート番号（例： 8080） |
| ProxyUid | 認証済みプロキシに使用するユーザー名 |
| ProxyPwd | ProxyUid パスワード |
| bqpath | これは、一括読み込みツール (Cloud SDK) にのみ適用されます。 </br> PATH 変数を使用しない場合や、google-cloud-sdk ディレクトリを別の場所に移動する必要がある場合は、このオプションで、サーバー上の cloud sdk bin ディレクトリの正確なパスを指定できます。 |
