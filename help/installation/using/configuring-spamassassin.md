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
>一部の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合です。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。

## 概要 {#overview}

SpamAssassin は、望ましくない E メールをフィルターするように設計されたソフトウェアの一部です。 Adobe Campaignは、このソフトウェアと組み合わせて、E メールにスコアを割り当て、配信が開始される前にメッセージが望ましくないと見なされる可能性があるかどうかを判断できます。 これをおこなうには、SpamAssassin をAdobe Campaignのアプリケーションサーバーにインストールして設定し、一定数の追加の Perl モジュールを動作させる必要があります。

この章で説明する SpamAssassin のデプロイと統合は、デフォルトのソフトウェアインストールと、フィルタリングとスコアリングルールに基づいています。これは、変更や最適化をおこなわずに SpamAssassin が提供するものです。 スコアのアトリビューションとメッセージの選定は、SpamAssassin オプションの設定とフィルタールールのみに基づいています。 ネットワーク管理者は、自社のニーズに合わせてネットワーク管理者を適応させます。

>[!IMPORTANT]
>
>SpamAssassin によって望ましくない E メールの認定は、完全にフィルタリングとスコアルールに基づいています。
>
>したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも 1 日に 1 回更新する必要があります。
>
>この更新は、SpamAssassin をホストするサーバー管理者の責任です。

Adobe Campaignで SpamAssassin を使用すると、Adobe Campaignから送信された E メールを受信したときに SpamAssassin を使用するメールサーバーが起こり得る動作を示すことができます。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーが、Adobe Campaignから送信されるメッセージを望ましくないと見なす可能性があります。

SpamAssassin とそのモジュールを Perl にデプロイするには、HTTP 接続（TCP/80 フロー）を介したインターネットアクセスを備えたAdobe Campaignアプリケーションサーバーが必要です。

## Windows マシンへのインストール {#installing-on-a-windows-machine}

Windows に SpamAssassin をインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順に従います。

1. SpamAssassin のインストール
1. SpamAssassin のAdobe Campaignへの統合

### SpamAssassin のインストール {#installing-spamassassin}

1. ユーザーの資格情報を使用して、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html) に接続します。 ソフトウェアの配布について詳しくは、[ このページ ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja) を参照してください。
1. **Neolane Spam Assassin（Windows インストール）(2.0)** ファイル (neolane_spamassassin.2.0.zip) をダウンロードします。
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字のいずれかで構成されている場合は、任意の場所にファイルを解凍できます。**`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めないでください。

1. ファイルを解凍したファイルに移動し、**run_me.bat** ファイルをダブルクリックしてインストールスクリプトを起動します。

   Windows シェルが表示され、数秒間表示され続ける場合は、インストールと更新が完了するまで待ってから、[**Enter**] をクリックします。

   Windows シェルが表示されない場合や、表示されない場合は、次の手順に従い、 **portableShell.bat** ファイルをダブルクリックして Windows シェルを表示し、**spamassassin.zip** ファイルが解凍されたフォルダーに対応するシェルパスを確認します。 そうでない場合は、**cd** コマンドを使用してアクセスします。

   **run_me.bat** と入力し、**Enter** をクリックして、インストールと更新のプロセスを開始します。 この操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**:更新が実行されました。
   * **1**:新しい更新プログラムはありません。
   * **2**:新しい更新プログラムはありません。
   * **3**:前回の検証中に更新に失敗しました。
   * **4** 以上：エラーが発生しました。

1. SpamAssassin のインストールが成功したことを確認するには、次の手順に従って、GTUBE テスト（未承諾の一括電子メールの汎用テスト）を使用します。

   1. テキストファイルを作成し、**C:\TestSpamMail.txt** の下に保存します。
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

   1. **portableShell.bat** ファイルをダブルクリックして Windows シェルを表示し、次のコマンドを実行します（または、**spamassassin.zip** ファイルを解凍する際に、「`<root>`」で作成したフォルダを指定します）。

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト用 E メールの内容は、SpamAssassin による 1,000 ポイントのスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssassin のAdobe Campaignへの統合 {#integrating-spamassassin-into-adobe-campaign}

1. **`[INSTALL]/conf/serverConf.xml`** ファイルを編集します。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。
1. **Web** ノードの **spamCheck** 要素&#39; **command** 属性の値を変更します。 これをおこなうには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   **[!UICONTROL Adobe Campaign]** サービスを停止して起動します。

1. Adobe Campaignで SpamAssassin の統合を確認するには、GTBUE テスト（未承諾の一括電子メール用の汎用テスト）を使用します。

   **portableshell.bat** ファイルをダブルクリックします。 このトリガーは、Windows シェルの表示を示します。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト用 E メールトリガーの内容は、SpamAssassin によって割り当てられた 1,000 ポイントです。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. SpamAssassin のフィルタリングおよびスコアリングルールの更新

   フィルタリングとスコアリングルールを初めて更新する場合は、 **portableShell.bat** を起動し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングルールとスコアリングルールの自動更新を実行するには、スケジュールされたシステムタスクで次の同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linux マシンへのインストール {#installing-on-a-linux-machine}

### Debian でのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用して Perl と SpamAssassin をインストールします。

   ```
   apt-get install spamassassin libxml-writer-perl
   ```

* **serverConf.xml** ファイル（`/usr/local/[INSTALL]/nl6/conf/` から入手可能）で、**spamCheck** の行を次のように変更します。

   ```
   <spamCheck command="perl
   /usr/local/[NSTALL]/nl6/bin/spamcheck.pl"/>
   ```

### RHEL/CentOS でのインストール手順 {#installation-steps-in-rhel-centos}

必要に応じて、Perl をインストールし、CPAN を使用してパッケージを回復します。

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

フィルタールールは、**sa-update** ツールを使用して自動的に更新できます。 詳しくは、公式の SpamAssassin の Web サイト [https://spamassassin.apache.org/](https://spamassassin.apache.org/) を参照してください。

Debian では、更新は毎日自動的におこなわれます。

そうでない場合（Debian を手動でインストールする場合など）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して、**crontab** にこのスクリプトを挿入します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linux でのパフォーマンスを向上させるには、**/etc/spamassassin/local.cf** ファイルを編集し、ファイルの最後に次の行を追加します。

```
dns_available no
```
