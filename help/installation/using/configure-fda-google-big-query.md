---
product: campaign
title: Google BigQuery へのアクセスの設定
description: FDA でGoogle BigQuery へのアクセスを設定する方法を説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: ebaad59f-0607-4090-92d0-e457fbf9a348
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 7%

---

# Google BigQuery へのアクセスの設定 {#configure-fda-google-big-query}



Adobe Campaign Classic **Federated Data Access** （FDA）オプションを使用すると、外部データベースに保存されている情報を処理できます。 [!DNL Google BigQuery] へのアクセスを設定するには、次の手順に従います。

1. [Windows](#google-windows) または [Linux](#google-linux) での [!DNL Google BigQuery] の設定
1. Adobe Campaign Classicで [!DNL Google BigQuery] [ 外部アカウント ](#google-external) を設定します
1. [Windows](#bulk-load-windows) または [Linux](#bulk-load-linux) で [!DNL Google BigQuery] コネクタの一括読み込みを設定

>[!NOTE]
>
> [!DNL Google BigQuery] コネクタは、ホスト型、ハイブリッドおよびオンプレミスのデプロイメントで使用できます。 詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Windows でのGoogle BigQuery {#google-windows}

### Windows で設定されたドライバ {#driver-window}

1. [Windows 用 ODBC ドライバ ](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers) をダウンロードします。

1. Windows で ODBC ドライバを設定します。 詳しくは、[このページ](https://storage.googleapis.com/simba-bq-release/jdbc/Simba%20JDBC%20Driver%20for%20Google%20BigQuery%20Install%20and%20Configuration%20Guide.pdf)を参照してください。

1. [!DNL Google BigQuery] コネクタを動作させるには、Adobe Campaign Classicが接続するために次のパラメーターを必要とします。

   * **[!UICONTROL プロジェクト]**：既存のプロジェクトを作成または使用します。

     詳しくは、[このページ](https://cloud.google.com/resource-manager/docs/creating-managing-projects)を参照してください。

   * **[!UICONTROL サービスアカウント]**：サービスアカウントを作成します。

     詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-accounts)を参照してください。

   * **[!UICONTROL キーファイル パス]**: **[!UICONTROL サービス アカウント]** には、ODBC を介した [!DNL Google BigQuery] 接続のために **[!UICONTROL キーファイル]** が必要です。

     詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)を参照してください。

   * **[!UICONTROL データセット]**: **[!UICONTROL データセット]** は、ODBC 接続ではオプションです。 すべてのクエリはテーブルが配置されているデータセットを提供する必要があるので、Adobe Campaign Classicの FDA コネクタでは **[!UICONTROL データセット]** の指定 [!DNL Google BigQuery] 必須です。

     詳しくは、[このページ](https://cloud.google.com/bigquery/docs/datasets)を参照してください。

1. Adobe Campaign Classicで、[!DNL Google BigQuery] 外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[ この節 ](#google-external) を参照してください。

### Windows での一括読み込みの設定 {#bulk-load-window}

>[!NOTE]
>
>Google Cloud SDKを機能させるには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。この [ ページ ](https://www.python.org/downloads/) を参照してください。

一括読み込みユーティリティを使用すると、転送が高速になります。これはGoogle Cloud SDKを通じて実現されます。

1. この [ ページ ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) から Windows 64 ビット（x86_64）アーカイブをダウンロードし、対応するディレクトリに抽出します。

1. `google-cloud-sdk\install.sh` スクリプトを実行します。 パス変数の設定をそのまま使用する必要があります。

1. インストール後、パス変数 `...\google-cloud-sdk\bin` が設定されていることを確認します。 追加しない場合は、手動で追加します。

1. `..\google-cloud-sdk\bin\bq.cmd` ファイルに、Python インストールの場所にリダイレクトする `CLOUDSDK_PYTHON` ローカル変数を追加します。

   例：

   ![](assets/google-big-query_1.png)

1. 変更内容を反映するには、Adobe Campaign Classicを再起動します。

## Linux 上のGoogle BigQuery {#google-linux}

### Linux で設定されたドライバ {#driver-linux}

ドライバを設定する前に、スクリプトとコマンドは root ユーザーが実行する必要があることに注意してください。 スクリプトの実行中にGoogle DNS 8.8.8.8 を使用することもお勧めします。

Linux で [!DNL Google BigQuery] を設定するには、次の手順に従います。

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

1. インストール前のシステム更新：

   * Red Hat/CentOS:

     ```
     # install unixODBC driver manager
     yum install -y unixODBC
     ```

   * Debian の場合

     ```
     # install unixODBC driver manager
     apt-get install -y odbcinst1debian2 libodbc1 odbcinst unixodbc
     ```

1. スクリプトを実行する前に、次のように – help 引数を指定すると、詳細な情報を取得できます。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_odbc-setup.sh --help
   ```

1. スクリプトがあるディレクトリにアクセスし、ルートユーザーとして次のスクリプトを実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_odbc-setup.sh
   ```

### Linux での一括読み込みの設定 {#bulk-load-linux}

>[!NOTE]
>
>Google Cloud SDKを機能させるには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。この [ ページ ](https://www.python.org/downloads/) を参照してください。

一括読み込みユーティリティを使用すると、転送が高速になります。これはGoogle Cloud SDKを通じて実現されます。

1. ODBC をインストールする前に、Linux ディストリビューションに次のパッケージがインストールされていることを確認します。

   * Red Hat/CentOS:

     ```
     yum update
     yum upgrade
     yum install -y python3
     ```

   * Debian の場合

     ```
     apt-get update
     apt-get upgrade
     apt-get install -y python3
     ```

1. スクリプトが配置されているディレクトリにアクセスし、次のスクリプトを実行します。

   ```
   cd /usr/local/neolane/nl6/bin/fda-setup-scripts
   ./bigquery_sdk-setup.sh
   ```

## Google BigQuery 外部アカウント {#google-external}

Adobe Campaign Classic インスタンスを [!DNL Google BigQuery] 外部データベースに接続するには、[!DNL Google BigQuery] 外部アカウントを作成する必要があります。

1. Adobe Campaign Classic **[!UICONTROL エクスプローラー]** で、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]** をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. [!DNL Google BigQuery] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Google BigQuery]

   * **[!UICONTROL サービスアカウント]**：お使いの **[!UICONTROL サービスアカウント]** のメール。 詳しくは、[Google Cloud ドキュメント ](https://cloud.google.com/iam/docs/creating-managing-service-accounts) を参照してください。

   * **[!UICONTROL プロジェクト]**: **[!UICONTROL プロジェクト]** の名前 詳しくは、[Google Cloud ドキュメント ](https://cloud.google.com/resource-manager/docs/creating-managing-projects) を参照してください。

   * **[!UICONTROL キーファイルパス]**:
      * **[!UICONTROL サーバーにキーファイルをアップロード]**:Adobe Campaign Classicからキーをアップロードする場合は、**[!UICONTROL ここをクリックしてアップロード]** を選択します。

      * **[!UICONTROL キーファイルパスを手動で入力]**：既存のキーを使用する場合は、このフィールドに絶対パスをコピーして貼り付けます。

   * **[!UICONTROL データセット]**: **[!UICONTROL データセット]** の名前 詳しくは、[Google Cloud ドキュメント ](https://cloud.google.com/bigquery/docs/datasets-intro) を参照してください。

   ![](assets/google-big-query.png)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|:-:|:-:|
| ProxyType | ODBC およびSDK コネクタ経由で BigQuery に接続するために使用されるプロキシの種類です。 現在、</br>HTTP （デフォルト）、http_no_tunnel、socks4、socks5 がサポートされています。 |
| ProxyHost | プロキシにアクセスできるホスト名または IP アドレス。 |
| ProxyPort | プロキシが実行されているポート番号（例：8080） |
| ProxyUid | 認証済みプロキシに使用するユーザー名 |
| ProxyPwd | ProxyUid パスワード |
| bqpath | これは、一括読み込みツール（Cloud SDK）にのみ適用されます。 </br> PATH 変数の使用を避ける場合や、google-cloud-sdk ディレクトリを別の場所に移動する必要がある場合は、このオプションを使用して、サーバー上の cloud sdk bin ディレクトリへの正確なパスを指定できます。 |
| GCloudConfigName | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツールのみ（Cloud SDK）に適用されることに注意してください。</br> Google Cloud SDKは、設定を使用して BigQuery テーブルにデータを読み込みます。 `accfda` という名前の設定は、データを読み込むためのパラメーターを格納します。 ただし、このオプションを使用すると、ユーザーは設定に別の名前を指定できます。 |
| GCloudDefaultConfigName | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツールのみ（Cloud SDK）に適用されることに注意してください。</br> アクティブなGoogle Cloud SDK設定は、最初にアクティブなタグを新しい設定に転送しないと、削除できません。 データを読み込むためのメイン設定を再作成するには、この一時的な設定が必要です。 一時設定のデフォルト名は `default` です。これは必要に応じて変更できます。 |
| GCloudRecreateConfig | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツールのみ（Cloud SDK）に適用されることに注意してください。</br> `false` に設定すると、一括読み込みメカニズムは、Google Cloud SDK設定を再作成、削除、変更しようとしません。 代わりに、マシン上の既存の設定を使用してデータの読み込みを続行します。 この機能は、他の操作がGoogle Cloud SDK設定に依存している場合に役立ちます。 </br> 適切な設定を行わないでこのエンジンオプションを有効にすると、一括読み込みメカニズムは警告メッセージを表示します：`No active configuration found. Please either create it manually or remove the GCloudRecreateConfig option`。 それ以上のエラーを防ぐために、デフォルトの ODBC 配列の挿入バルクロードメカニズムを使用して、に戻ります。 |

