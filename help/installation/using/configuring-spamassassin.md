---
product: campaign
title: SpamAssassin の設定
description: SpamAssassin の設定
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 1f1004e2-dcd2-4ec5-98ec-720c205646d5
source-git-commit: 32f55d02920b0104198f809b1be0a91306a4d9e4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# SpamAssassin の設定{#configuring-spamassassin}

![](../../assets/v7-only.svg)

>[!NOTE]
>
>一部の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合などです。 様々なデプロイメントの詳細については、[モデルのホスティング](../../installation/using/hosting-models.md)の節または[このページ](../../installation/using/capability-matrix.md)を参照してください。

## 概要 {#overview}

SpamAssassinは、望ましくないEメールをフィルターするように設計されたソフトウェアの一部です。 Adobe Campaignとこのソフトウェアを組み合わせて、Eメールにスコアを割り当て、配信が開始される前にメッセージが望ましくないと見なされる可能性があるかどうかを判断できます。 これを行うには、SpamAssassinをAdobe Campaignのアプリケーションサーバーにインストールして設定し、一定数の追加のPerlモジュールを動作させる必要があります。

この章で説明するSpamAssassinのデプロイと統合は、デフォルトのソフトウェアインストールと、フィルタリングとスコアリングルールに基づいています。これは、変更や最適化をおこなわずにSpamAssassinが提供するものです。 スコアのアトリビューションとメッセージの選定は、SpamAssassinオプションの設定とフィルタリングルールにのみ基づいています。 ネットワーク管理者は、自社のニーズに合わせてネットワーク管理者を適応させます。

>[!IMPORTANT]
>
>SpamAssassinによって望ましくないEメールの認定は、完全にフィルタリングとスコアルールに基づいています。
>
>したがって、SpamAssassinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日に1回更新する必要があります。
>
>この更新は、SpamAssassinをホストするサーバー管理者の責任です。

Adobe CampaignでSpamAssassinを使用すると、Adobe Campaignから送信されたEメールを受信したときにSpamAssassinを使用するメールサーバーが起こりうる動作を示します。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーは、Adobe Campaignから送信されるメッセージを引き続き望ましくないものと見なす可能性があります。

SpamAssassinとそのモジュールをPerlにデプロイするには、HTTP接続（TCP/80フロー）を介したインターネットアクセスを備えたAdobe Campaignアプリケーションサーバーが必要です。

## Windowsマシンへのインストール {#installing-on-a-windows-machine}

Adobe Campaignとの統合を有効にするためにWindowsにSpamAssassinをインストールして設定するには、次の手順に従います。

1. SpamAssassinのインストール
1. SpamAssassinをAdobe Campaignに統合

### SpamAssassinのインストール {#installing-spamassassin}

1. ユーザーの資格情報を使用して、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html?lang=ja)に接続します。 ソフトウェアの配布について詳しくは、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja?lang=en)を参照してください。
1. **Neolane Spam Assassin（Windowsインストール）(2.0)**&#x200B;ファイル(neolane_spamassassin.2.0.zip)をダウンロードします。
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字のいずれかで構成されている場合は、任意の場所にファイルを解凍できます。**`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めないでください。

1. ファイルを解凍したファイルに移動し、**run_me.bat**&#x200B;ファイルをダブルクリックしてインストールスクリプトを起動します。

   Windowsシェルが表示され、数秒間表示され続ける場合は、インストールが完了して更新が完了するまで待ってから、**Enter**&#x200B;をクリックします。

   Windowsシェルが表示されない、または表示されない場合は、次の手順に従います。 **portableShell.bat**&#x200B;ファイルをダブルクリックしてWindowsシェルを表示し、**spamassassin.zip**&#x200B;ファイルが解凍されたフォルダーに対応するシェルパスを確認します。 そうでない場合は、**cd**&#x200B;コマンドを使用してアクセスします。

   **run_me.bat**&#x200B;と入力し、**Enter**&#x200B;をクリックして、インストールと更新のプロセスを開始します。 この操作では、更新の結果を示すために、次のいずれかの値を返します。

   * **0**:更新が実行されました。
   * **1**:新しい更新プログラムはありません。
   * **2**:新しい更新プログラムはありません。
   * **3**:前の検証中に更新に失敗しました。
   * **4** 以上：エラーが発生しました。

1. SpamAssassinのインストールが成功したことを確認するには、次の手順に従って、GTUBEテスト（未承諾の一括電子メールの汎用テスト）を使用します。

   1. テキストファイルを作成し、**C:\TestSpamMail.txt**&#x200B;の下に保存します。
   1. ファイルに次のコンテンツを挿入します。

      ```
      Subject: Test Spam Mail (GTUBE)
      Message-ID: <1010101@example.net>
      Date: MM-DD-YY
      From: Sender <sender@example.net>
      To: Recipient <recipient@example.net>
      Precedence: junk
      MIME-Version: 1.0
      Content-Type: text/plain; charset=us-ascii
      Content-Transfer-Encoding: 7bit
      
      XJS*C4JDBQADN1.NSBN3*2IDNEN*GTUBE-STANDARD-ANTI-UBE-TEST-EMAIL*C.34X
      ```

   1. **portableShell.bat**&#x200B;ファイルをダブルクリックしてWindowsシェルを表示し、次のコマンドを実行します（または、**spamassassin.zip**&#x200B;ファイルを解凍する際に、「`<root>`」は作成したフォルダーを指定します）。

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト用Eメールのトリガーは、SpamAssassinによる1,000ポイントのスコアです。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssassinのAdobe Campaignへの統合 {#integrating-spamassassin-into-adobe-campaign}

1. **`[INSTALL]/conf/serverConf.xml`**&#x200B;ファイルを編集します。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。
1. **Web**&#x200B;ノードの&#x200B;**spamCheck**&#x200B;要素の&#x200B;**command**&#x200B;属性の値を変更します。 これをおこなうには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   **[!UICONTROL Adobe Campaign]**&#x200B;サービスを停止し、開始します。

1. Adobe CampaignでSpamAssassinの統合を確認するには、GTBUEテスト（未承諾の一括電子メール用の汎用テスト）を使用します。

   **portableshell.bat**&#x200B;ファイルをダブルクリックします。 このトリガーは、Windowsシェルの表示を示します。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト用Eメールの内容は、SpamAssassinによって割り当てられた1,000ポイントをトリガーします。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. SpamAssassinのフィルタリングおよびスコアルールの更新

   フィルタリングとスコアリングルールを初めて更新する場合は、 **portableShell.bat**&#x200B;を起動し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングルールとスコアリングルールの自動更新を実行するには、スケジュールされたシステムタスクで同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linuxマシンへのインストール {#installing-on-a-linux-machine}

### Debianでのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用してPerlとSpamAssassinをインストールします。

   ```
   apt-get install spamassassin libxml-writer-perl
   ```

* **serverConf.xml**&#x200B;ファイル（`/usr/local/[INSTALL]/nl6/conf/`から入手可能）で、**spamCheck**&#x200B;行を次のように変更します。

   ```
   <spamCheck command="perl
   /usr/local/[NSTALL]/nl6/bin/spamcheck.pl"/>
   ```

### RHEL/CentOSでのインストール手順 {#installation-steps-in-rhel-centos}

必要に応じて、Perlをインストールし、CPANを使用してパッケージを回復します。

```
cpan Digest::SHA1
cpan HTML::Parser
cpan Net::DNS
cpan Mail::SPF 
cpan XML::LibXML
cpan XML::Writer
cpan Mail::SpamAssassin
```

### フィルタールールの更新 {#updating-filter-rules}

フィルタールールは、**sa-update**&#x200B;ツールを使用して自動的に更新できます。 詳しくは、公式のSpamAssassin Webサイト[https://spamassassin.apache.org/](https://spamassassin.apache.org/)を参照してください。

Debianでは、更新は毎日自動的におこなわれます。

そうでない場合（例えば、Debianが手動でインストールされている場合）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して、**crontab**&#x200B;にこのスクリプトを挿入します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linuxでのパフォーマンスを向上させるには、**/etc/spamassassin/local.cf**&#x200B;ファイルを編集し、ファイルの最後に次の行を追加します。

```
dns_available no
```
