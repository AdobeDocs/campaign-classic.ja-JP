---
title: Campaignサーバーの設定
seo-title: Campaignサーバーの設定
description: Campaignサーバーの設定
seo-description: null
page-status-flag: never-activated
uuid: a1fadad2-e888-4dd8-bc1f-04df16ba7d46
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: f296676e-3bf1-47da-8239-f5ae54e52fc0
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 4869eb41f942a89c48bc213913c44b70ae777bfc

---


# Campaign server configuration{#campaign-server-configuration}

以下の節では、ほとんどのセットアップでAdobe Campaignを効率的に運用できるようにする、必須のサーバー設定について詳しく説明します。

追加の設定は、Campaignサーバーの設 [定で提供されます](../../installation/using/configuring-campaign-server.md)。

>[!NOTE]
>
>サーバー側の設定は、アドビがホストするデプロイメントに対してのみ実行できます。 各デプロイメントの詳細については、「ホスティングモデル [」の節またはこの記事を参照し](../../installation/using/hosting-models.md) てください [](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)。

## 内部識別子 {#internal-identifier}

内部識 **別子は** 、インストール、管理、メンテナンスの目的で使用する技術的なログインです。 このログインはインスタンスに関連付けられていません。

このログインを使用して接続されたオペレーターは、すべてのインスタンスに対するすべての権限を持ちます。 新しいインストールの場合、このログインにはパスワードが含まれません。 このパスワードは手動で定義する必要があります。

次のコマンドを使用します。

```
nlserver config -internalpassword
```

次の情報が表示されます。 パスワードを入力し、確認します。

```
17:33:57 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
Enter the current password.
Password:
Enter the new password.
Password: XXXX
Confirmation: XXXX
17:34:02 >   Password successfully changed for account 'internal' (authentication mode 'nl')
```

## 設定ファイル {#configuration-files}

設定ファイルは、Adobe Campaignのインスト **ールフォルダー** confフォルダーに保存されます。 設定は2つのファイルに分散されます。

* **`config-<instance>.xml`** ( **instanceは** 、インスタンスの名前です)。インスタンスの特定の設定。 サーバーを複数のインスタンス間で共有する場合は、各インスタンスに固有のパラメーターを関連ファイルに入力してください。
* **serverConf.xml**:すべてのインスタンスの一般設定。 このファイルは、Adobe Campaignサーバーの技術パラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部の説明を以下に示します。 使用可能なすべてのパラメータを表示するには、ファイル自体を参照します。 異なるノードとパラメーター、およびこの節に示 [します](../../installation/using/the-server-configuration-file.md)。

Adobe Campaignデータ(ログ、ダウンロ&#x200B;**ード** 、リダイレクトなど)のストレージディレクトリ（varディレクトリ）を設定できます。 これを行うには、 **XTK_VAR_DIR** システム変数を使用します。

* Windowsでは、システム変数 **XTK_VAR_DIR**

   ```
   D:\log\AdobeCampaign
   ```

* Linuxでは、 **customer.shファイルに移動し** 、次のことを示します。 **XTK_VAR_DIR=/app/log/AdobeCampaignをエクスポートします**。

   For more on this, refer to [Personalizing parameters](../../installation/using/installing-packages-with-linux.md#personalizing-parameters).

## プロセスの有効化 {#enabling-processes}

サーバー上のAdobe Campaignプロセスは、 **config-default.xmlとファイルを使用して有効(および無効** )にな **`config-<instance>.xml`** ります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合、 **nlserver config -reload** コマンドを実行する必要があります。

プロセスには2つのタイプがあります。マルチインスタンスとシングルインスタンス

* **マルチインスタンス**:すべてのインスタンスに対して1つのプロセスが開始されます。 これは、web、 **syslogd**、 **trackinglogdの各プロ** セスの場合 **** です。

   有効化は、 **config-default.xmlファイルから設定できます** 。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）を行うようにAdobe Campaignサーバーを宣言する場合：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linuxの **vi** コマンドを使用してファイルを編集します。 任意の **.txtまたは** .xmlエディターを使用して編集できます **** 。

* **モノラルインスタンス**:各インスタンスに対して1つのプロセスが開始されます(モジュール： **mta, wfserver****,** inMail **,** sms ta **,****** stat stat )

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

## 配信設定 {#delivery-settings}

配信パラメーターは、 **serverConf.xmlフォルダーで設定する必要があります** 。

* **DNS構成**:以降のMTAモジュールが行うMXタイプDNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定し **`<dnsconfig>`** ます。

   >[!NOTE]
   >
   >Windowsでのイ **ンストールには** 、nameServersパラメーターが必要です。 Linuxでのインストールの場合は、空のままにしておく必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

このファイルで使用できるその他の配信パラメーターは、配信パラメーターの個人 [化に記載されていま](../../installation/using/configuring-campaign-server.md#personalizing-delivery-parameters)す。

「電子メールの配信 [品質」も参照](../../installation/using/email-deliverability.md)。
