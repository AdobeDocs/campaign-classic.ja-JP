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



Adobe Campaign Classicの使用 **連合データアクセス** （FDA）外部データベースに保存された情報を処理するオプション。 へのアクセスを設定するには、次の手順に従います [!DNL Google BigQuery].

1. 設定 [!DNL Google BigQuery] 日付： [Windows](#google-windows) または [Linux](#google-linux)
1. の設定 [!DNL Google BigQuery] [外部アカウント](#google-external) Adobe Campaign Classic内
1. の設定 [!DNL Google BigQuery] コネクタの一括読み込み： [Windows](#bulk-load-windows) または [Linux](#bulk-load-linux)

>[!NOTE]
>
> [!DNL Google BigQuery] コネクタは、ホスト型、ハイブリッドおよびオンプレミスのデプロイメントで使用できます。 詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Windows でのGoogle BigQuery {#google-windows}

### Windows で設定されたドライバ {#driver-window}

1. をダウンロード [Windows 用 ODBC ドライバ](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers).

1. Windows で ODBC ドライバを設定します。 詳しくは、[このページ](https://storage.googleapis.com/simba-bq-release/jdbc/Simba%20JDBC%20Driver%20for%20Google%20BigQuery%20Install%20and%20Configuration%20Guide.pdf)を参照してください。

1. の場合 [!DNL Google BigQuery] コネクタを動作させるには、Adobe Campaign Classicが接続するために次のパラメーターが必要です。

   * **[!UICONTROL プロジェクト]**：既存のプロジェクトを作成または使用します。

     詳しくは、[このページ](https://cloud.google.com/resource-manager/docs/creating-managing-projects)を参照してください。

   * **[!UICONTROL サービスアカウント]**：サービスアカウントを作成します。

     詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-accounts)を参照してください。

   * **[!UICONTROL キーファイルのパス]**：です **[!UICONTROL サービスアカウント]** が必要 **[!UICONTROL キーファイル]** の場合 [!DNL Google BigQuery] odbc 経由の接続。

     詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)を参照してください。

   * **[!UICONTROL データセット]**: **[!UICONTROL データセット]** ODBC 接続の場合はオプションです。 すべてのクエリは、テーブルが配置されているデータセットを提供する必要があるので、を指定します。 **[!UICONTROL データセット]** は次に対して必須です： [!DNL Google BigQuery] Adobe Campaign Classicの FDA コネクタ。

     詳しくは、[このページ](https://cloud.google.com/bigquery/docs/datasets)を参照してください。

1. Adobe Campaign Classicで、以下を設定できます [!DNL Google BigQuery] 外部アカウント。 外部アカウントの設定方法について詳しくは、次を参照してください。 [この節](#google-external).

### Windows での一括読み込みの設定 {#bulk-load-window}

>[!NOTE]
>
>Google Cloud SDK が機能するには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。こちらを参照してください [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、転送が高速になります。これはGoogle Cloud SDK を通じて実現されます。

1. このから Windows 64 ビット （x86_64） アーカイブをダウンロードします [ページ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) 対応するディレクトリに抽出します。

1. を実行 `google-cloud-sdk\install.sh` スクリプト。 パス変数の設定をそのまま使用する必要があります。

1. インストール後、パス変数を確認します。 `...\google-cloud-sdk\bin` が設定されています。 追加しない場合は、手動で追加します。

1. が含まれる  `..\google-cloud-sdk\bin\bq.cmd` ファイル、を追加 `CLOUDSDK_PYTHON` ローカル変数。Python インストールの場所にリダイレクトされます。

   例：

   ![](assets/google-big-query_1.png)

1. 変更内容を反映するには、Adobe Campaign Classicを再起動します。

## Linux 上のGoogle BigQuery {#google-linux}

### Linux で設定されたドライバ {#driver-linux}

ドライバを設定する前に、スクリプトとコマンドは root ユーザーが実行する必要があることに注意してください。 スクリプトの実行中にGoogle DNS 8.8.8.8 を使用することもお勧めします。

を設定 [!DNL Google BigQuery] linux の場合は、次の手順に従います。

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
>Google Cloud SDK が機能するには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。こちらを参照してください [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、転送が高速になります。これはGoogle Cloud SDK を通じて実現されます。

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

を作成する必要があります [!DNL Google BigQuery] Adobe Campaign Classic インスタンスをに接続するための外部アカウント [!DNL Google BigQuery] 外部データベース。

1. Adobe Campaign Classicから **[!UICONTROL エクスプローラー]**&#x200B;を選択し、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. [!DNL Google BigQuery] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Google BigQuery]

   * **[!UICONTROL サービスアカウント]**：のメール **[!UICONTROL サービスアカウント]**. 詳しくは、次を参照してください。 [Google Cloud ドキュメント](https://cloud.google.com/iam/docs/creating-managing-service-accounts).

   * **[!UICONTROL プロジェクト]**：の名前 **[!UICONTROL プロジェクト]**. 詳しくは、次を参照してください。 [Google Cloud ドキュメント](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

   * **[!UICONTROL キーファイルのパス]**:
      * **[!UICONTROL サーバーにキーファイルをアップロード]**：を選択 **[!UICONTROL ここをクリックしてアップロード]** Adobe Campaign Classicからキーをアップロードする場合。

      * **[!UICONTROL 手動でキーファイルパスを入力]**：既存のキーを使用する場合は、このフィールドに絶対パスをコピーして貼り付けます。

   * **[!UICONTROL データセット]**：の名前 **[!UICONTROL データセット]**. 詳しくは、次を参照してください。 [Google Cloud ドキュメント](https://cloud.google.com/bigquery/docs/datasets-intro).

   ![](assets/google-big-query.png)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|:-:|:-:|
| ProxyType | ODBC および SDK コネクタ経由で BigQuery に接続するために使用されるプロキシの種類です。 </br>現在、HTTP （デフォルト）、http_no_tunnel、socks4、socks5 がサポートされています。 |
| ProxyHost | プロキシにアクセスできるホスト名または IP アドレス。 |
| ProxyPort | プロキシが実行されているポート番号（例：8080） |
| ProxyUid | 認証済みプロキシに使用するユーザー名 |
| ProxyPwd | ProxyUid パスワード |
| bqpath | なお、これは一括読み込みツール（Cloud SDK）にのみ適用されます。 </br> PATH 変数の使用を避ける場合や、google-cloud-sdk ディレクトリを別の場所に移動する必要がある場合は、このオプションを使用して、サーバー上の cloud sdk bin ディレクトリへの正確なパスを指定できます。 |
| GCloudConfigName | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツール（Cloud SDK）にのみ適用されることに注意してください。</br> Google Cloud SDK は、設定を使用して BigQuery テーブルにデータを読み込みます。 という名前の設定 `accfda` データを読み込むためのパラメーターを格納します。 ただし、このオプションを使用すると、ユーザーは設定に別の名前を指定できます。 |
| GCloudDefaultConfigName | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツール（Cloud SDK）にのみ適用されることに注意してください。</br> アクティブなGoogle Cloud SDK 設定は、最初にアクティブなタグを新しい設定に転送しない限り、削除できません。 データを読み込むためのメイン設定を再作成するには、この一時的な設定が必要です。 一時設定のデフォルト名はです。 `default`（必要に応じて変更できます）。 |
| GCloudRecreateConfig | これは、リリース 7.3.4 リリース以降に適用され、一括読み込みツール（Cloud SDK）にのみ適用されることに注意してください。</br> に設定されている場合 `false`の場合、一括読み込みメカニズムでは、Google Cloud SDK 設定を再作成、削除または変更しようとしません。 代わりに、マシン上の既存の設定を使用してデータの読み込みを続行します。 この機能は、他の操作がGoogle Cloud SDK 設定に依存している場合に役立ちます。 </br> 適切な設定を行わなくても、ユーザーがこのエンジンオプションを有効にすると、一括読み込みメカニズムによって警告メッセージが表示されます。 `No active configuration found. Please either create it manually or remove the GCloudRecreateConfig option`. それ以上のエラーを防ぐために、デフォルトの ODBC 配列の挿入バルクロードメカニズムを使用して、に戻ります。 |

