---
title: Campaign サーバーの設定
seo-title: Campaign サーバーの設定
description: Campaign サーバーの設定
seo-description: null
page-status-flag: never-activated
uuid: a1fadad2-e888-4dd8-bc1f-04df16ba7d46
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: f296676e-3bf1-47da-8239-f5ae54e52fc0
translation-type: tm+mt
source-git-commit: 3acf2359c74a3dc4b18c8976fee14dcbaf3fa510
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# Campaign サーバーの設定{#campaign-server-configuration}

次の節では、ほとんどのセットアップでAdobe Campaignを効率的に動作させるための必須のサーバ設定について説明します。

追加の設定は、「 [キャンペーンサーバーの](../../installation/using/configuring-campaign-server.md)設定」で行います。

>[!NOTE]
>
>サーバ側の設定は、Adobeがホストする配置に対してのみAdobeが実行できます。 各デプロイメントの詳細については、「 [ホスティングモデル](../../installation/using/hosting-models.md) 」の節または機能マトリックス [を参照してください](../../installation/using/capability-matrix.md)。

## 内部識別子 {#internal-identifier}

**internal** identifierは、インストール、管理、保守の目的で使用する技術的なログインです。 このログインは、インスタンスに関連付けられていません。

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

## 設定ファイル {#configuration-files}

設定ファイルは、Adobe Campaignのインストールフォルダーの **conf** フォルダーに保存されます。 設定は2つのファイルに分かれています。

* **`config-<instance>.xml`** ( **instance** はインスタンスの名前):インスタンスの特定の設定。 サーバを複数のインスタンス間で共有する場合は、各インスタンスに固有のパラメータを関連ファイルに入力してください。
* **serverConf.xml**:すべてのインスタンスの一般設定。 このファイルは、Adobe Campaignサーバーの技術的なパラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部については、以下で詳しく説明します。 ファイル自体を参照して、使用可能なすべてのパラメーターを表示します。 この [節に示す様々なノードとパラメーター](../../installation/using/the-server-configuration-file.md)。

Adobe Campaignデータ（ログ、ダウンロード、リダイレクトなど）のストレージディレクトリ(**var** directory)を設定できます。 これを行うには、 **XTK_VAR_DIR** システム変数を使用します。

* Windowsの場合、 **システム変数XTK_VAR_DIR** :

   ```
   D:\log\AdobeCampaign
   ```

* Linuxでは、 **customer.sh** ファイルに移動し、次のことを示します。 **export XTK_VAR_DIR=/app/log/AdobeCampaign**.

   For more on this, refer to [Personalizing parameters](../../installation/using/installing-packages-with-linux.md#personalizing-parameters).

## プロセスの有効化 {#enabling-processes}

サーバー上のAdobe Campaignプロセスは、 **config-default.xml** と **`config-<instance>.xml`** ファイルを介して有効（および無効）になります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合、 **nlserver config -reload** コマンドを実行する必要があります。

プロセスには次の2種類があります。マルチインスタンスとシングルインスタンスの両方を追加します。

* **マルチインスタンス**:すべてのインスタンスに対して1つの単一プロセスが開始されます。 これは、 **web**、 **syslogd** 、および **trackinglogd** プロセスの場合です。

   有効化は、 **config-default.xml** ファイルから設定できます。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）を行うAdobe Campaignサーバーの宣言：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linuxの **vi** コマンドを使用してファイルを編集します。 任意の **.txt** または **.xml** エディターを使用して編集できます。

* **モノラルインスタンス**:各インスタンスに対して1つのプロセスが開始されます(モジュール： **mta**, wfserver **,** inMail **, sms**, **sms stat** not ****)

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

配信パラメーターは、 **serverConf.xml** フォルダーで設定する必要があります。

* **DNS構成**:以降のMTAモジュールが行うMX型DNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定し **`<dnsconfig>`** ます。

   >[!NOTE]
   >
   >Windowsでのインストールには、 **nameServers** パラメーターが必要です。 Linuxでのインストールの場合は、空のままにしておく必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

このファイルで使用できる他の配信パラメーターは、 [個人化配信パラメーター](../../installation/using/configuring-campaign-server.md#personalizing-delivery-parameters)。

「 [電子メールの配信品質](../../installation/using/email-deliverability.md)」も参照してください。
