---
solution: Campaign Classic
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 95d0686c4ddeb4e25eb918ca92cbd6a0b1aa1f3c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 2%

---


# Campaign サーバーの設定{#campaign-server-configuration}

次の節では、ほとんどのセットアップでAdobe Campaignを効率的に動作させるための必須のサーバ設定について説明します。

[キャンペーンサーバーの設定](../../installation/using/configuring-campaign-server.md)には、追加の設定が用意されています。

>[!NOTE]
>
>サーバ側の設定は、Adobeがホストする配置に対してのみAdobeが実行できます。 各デプロイメントの詳細については、[ホスティングモデル](../../installation/using/hosting-models.md)の節または[機能マトリクス](../../installation/using/capability-matrix.md)を参照してください。

## 内部識別子{#internal-identifier}

**internal**&#x200B;識別子は、インストール、管理、メンテナンスの目的で使用する技術的なログインです。 このログインは、インスタンスに関連付けられていません。

このログインを使用して接続されたオペレーターは、すべてのインスタンスに対してすべての権限を持ちます。 新たにインストールした場合、このログインにはパスワードがありません。 このパスワードは手動で定義する必要があります。

次のコマンドを使用します。

```
nlserver config -internalpassword
```

次の情報が表示されます。 パスワードを入力して確認します。

```
17:33:57 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
Enter the current password.
Password:
Enter the new password.
Password: XXXX
Confirmation: XXXX
17:34:02 >   Password successfully changed for account 'internal' (authentication mode 'nl')
```

## 構成ファイル{#configuration-files}

設定ファイルは、Adobe Campaignのインストールフォルダーの&#x200B;**conf**&#x200B;フォルダーに保存されます。 設定は2つのファイルに分かれています。

* **`config-<instance>.xml`** ( **** instanceはインスタンスの名前):インスタンスの特定の設定。サーバを複数のインスタンス間で共有する場合は、各インスタンスに固有のパラメータを関連ファイルに入力してください。
* **serverConf.xml**:すべてのインスタンスの一般設定。このファイルは、Adobe Campaignサーバーの技術的なパラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部については、以下で詳しく説明します。 ファイル自体を参照して、使用可能なすべてのパラメーターを表示します。 この[セクション](../../installation/using/the-server-configuration-file.md)に示す、様々なノードとパラメーター。

Adobe Campaignデータ（ログ、ダウンロード、リダイレクトなど）のストレージディレクトリ（**var**&#x200B;ディレクトリ）を設定できます。 これを行うには、**XTK_VAR_DIR**&#x200B;システム変数を使用します。

* Windowsの場合、**XTK_VAR_DIR**&#x200B;システム変数に次の値を指定します

   ```
   D:\log\AdobeCampaign
   ```

* Linuxでは、**customer.sh**&#x200B;ファイルに移動し、次のことを示します。**XTK_VAR_DIR=/app/log/AdobeCampaign**&#x200B;をエクスポートします。

   詳しくは、[パーソナライズパラメーター](../../installation/using/installing-packages-with-linux.md#personalizing-parameters)を参照してください。

## プロセスを有効にする{#enabling-processes}

サーバー上のAdobe Campaignプロセスは、**config-default.xml**&#x200B;ファイルと&#x200B;**`config-<instance>.xml`**&#x200B;ファイルを介して有効（および無効）になります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合、**nlserver config -reload**&#x200B;コマンドを実行する必要があります。

プロセスには次の2種類があります。マルチインスタンスとシングルインスタンスの両方を追加します。

* **マルチインスタンス**:すべてのインスタンスに対して1つの単一プロセスが開始されます。**web**、**syslogd**、**trackinglogd**&#x200B;の各プロセスは、このように処理されます。

   有効化は、**config-default.xml**&#x200B;ファイルから設定できます。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）を行うAdobe Campaignサーバーの宣言：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linuxでは&#x200B;**vi**&#x200B;コマンドを使用してファイルを編集します。 **.txt**&#x200B;または&#x200B;**.xml**&#x200B;エディターを使用して編集できます。

* **モノラルインスタンス**:各インスタンスに対して1つのプロセスが開始されます(モジュール： **mta**, wfserver **,** inMail **, sand** stat  ****  **** smt)

   有効化は、インスタンスの設定ファイルを使用して設定できます。

   ```
   config-<instance>.xml
   ```

   配信用のサーバーの宣言、ワークフローインスタンスの実行、バウンスメールの回復：

   ```
   <mta autoStart="true" statServerAddress="localhost"/>
   <wfserver autoStart="true"/>  
   <inMail autoStart="true"/>
   <stat autoStart="true"/>
   ```

## 配信設定{#delivery-settings}

配信パラメーターは、**serverConf.xml**&#x200B;フォルダーで設定する必要があります。

* **DNS構成**:以 **`<dnsconfig>`** 降のMTAモジュールが行うMX型DNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定します。

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターは、Windowsでのインストールに必須です。 Linuxでのインストールの場合は、空のままにしておく必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

このファイルで使用できる他の配信パラメーターは、[Personalize配信ーのパラメーター](../../installation/using/configuring-campaign-server.md#personalizing-delivery-parameters)に記載されています。

[Eメール配信品質](../../installation/using/email-deliverability.md)も参照してください。
