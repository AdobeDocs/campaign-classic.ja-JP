---
title: スパムアサシンの設定
seo-title: スパムアサシンの設定
description: スパムアサシンの設定
seo-description: null
page-status-flag: never-activated
uuid: 327548c0-d621-4417-9fc9-b0bf30251dc0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: additional-configurations
discoiquuid: aa37bdc6-0f85-4eca-859f-e8b15083cfb5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: edb99a13d8b2f39f991e8ceb6718291d92504242

---


# スパムアサシンの設定{#configuring-spamassassin}

>[!NOTE]
>
>一部の設定は、アドビがホストするデプロイメントに対してのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合です。 各デプロイメントの詳細については、「ホスティングモデル」の節 [または](../../installation/using/hosting-models.md) 、この記事を参照 [してください](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)。

## 概要 {#overview}

SpamAssacinは、望ましくない電子メールをフィルターするように設計されたソフトウェアの一部です。 Adobe Campaignは、このソフトウェアと組み合わせて、電子メールにスコアを割り当て、配信が開始される前にメッセージが望ましくないと見なされるかどうかを判断できます。 これを行うには、SpamAssacinがAdobe Campaignのアプリケーションサーバーにインストールされ、設定されている必要があります。また、Perlモジュールを一定数使用しないと動作しません。

本章で説明するSpamAssacsinの展開と統合は、フィルタリングとスコアリングのルールと同様、デフォルトのソフトウェアインストールに基づいており、変更や最適化を行うことなくSpamAssignが提供します。 スコアアトリビューションとメッセージの資格は、SpamAssignオプションの設定とフィルタールールのみに基づいています。 ネットワーク管理者は、自社のニーズに合わせてネットワークを調整する責任を負います。

>[!CAUTION]
>
>SpamAssacsinが望ましくない電子メールの資格は、完全にフィルタリングとスコアリングルールに基づいています。
>
>したがって、SpamAssacsinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するには、これらのルールを少なくとも1日に1回更新する必要があります。
>
>この更新は、SpamAssacinをホストするサーバー管理者の責任です。

SpamAssicinをAdobe Campaignで使用すると、Adobe Campaignから送信された電子メールを受信したときにSpamAssicinを使用するメールサーバーで発生する可能性がある動作を示すことができます。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーでは、Adobe Campaignから送信されるメッセージが望ましくないと引き続き考慮される可能性があります。

PerlにSpamAssacsinとそのモジュールをデプロイするには、HTTP接続（TCP/80フロー）を介したインターネットアクセスを備えたAdobe Campaignアプリケーションサーバーが必要です。

## Windowsマシンへのインストール {#installing-on-a-windows-machine}

WindowsにSpamAssacsinをインストールしてAdobe Campaignとの統合を有効にするには、次の手順を適用します。

1. SpamAssacinのインストール
1. SpamAssacsinをAdobe Campaignに統合

### SpamAssacinのインストール {#installing-spamassassin}

1. ユーザー資格情報を使 [用して](http://support.neolane.net) 、エクストラネットポータルに接続します。
1. ダウンロードセン **ターに移動し** 、ページを参照して「ツール」セクション **を探します** 。
1. スパムア **サシン（Windowsインストール）(1.0)ファイルをダウンロードします** 。
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字で構成されている場合は、必要に応じてファイルを解凍することができます。 **`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めることはできません。

1. ファイルの解凍先のファイルに移動し、 **run_me.batファイルをダブルクリックして、インストールスクリプトを起動します** 。

   Windowsシェルが表示され、数秒間表示が続く場合は、インストールが完了して更新が完了するまで待ってから、[ **Enter]をクリックします**。

   Windowsシェルが表示されない場合、または表示されない場合は、次の手順に従って **portableShell.bat** ファイルをダブルクリックし、Windowsシェルを表示し、Shellパスが、 **spamassin.zip** ファイルの解凍先フォルダーに対応していることを確認します。 そうでない場合は、 **cd** .

   run_me.bat **と入力し、「** Enter **** 」をクリックして、インストールと更新のプロセスを開始します。 この操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**:更新が実行されました。
   * **1**:新しい更新プログラムはありません。
   * **2**:新しい更新はありません。
   * **3**:前回の検証中に更新に失敗しました。
   * **4** 以上：エラーが発生しました。

1. SpamAssacinのインストールが正常に完了したことを確認するには、次の手順を使用してGTUBEテスト（非要請バルク電子メールの汎用テスト）を使用します。

   1. テキストファイルを作成し、C:\TestSpamMail.txtの下に保存 **します**。
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

   1. portableShell.batファイルをダブルクリックして **Windowsシェルを表示し、次のコマンドを起動します(または、「** 」は、spamassignin.zipファイルの解凍時に作成したフォルダ`<root>`ーを指定します **** )。

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト用電子メールのコンテンツは、SpamAssicinによる1,000ポイントスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssacinのAdobe Campaignへの統合 {#integrating-spamassassin-into-adobe-campaign}

1. ファイルを編集 **`[INSTALL]/conf/serverConf.xml`** します。 serverConf.xmlで使用可能なすべてのパ **ラメーターを** 、この節に示 [します](../../installation/using/the-server-configuration-file.md)。
1. **Web** ノードのspamCheck **要素のcommand属** 性の値 **** を変更します。 これを行うには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   サービスを停止し、開始 **[!UICONTROL Adobe Campaign]** します。

1. Adobe CampaignでSpamAssacsinの統合を確認するには、GTBUEテスト（未請求バルク電子メールの汎用テスト）を使用します。

   portableshell.batファイルをダブ **ルクリックします** 。 これにより、Windowsシェルの表示がトリガされます。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト用電子メールのコンテンツは、SpamAssacinによって割り当てられた1,000ポイントをトリガーします。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. スパムアサシンのフィルタリングとスコアリングルールの更新

   フィルタリングとスコアリングルールの初期更新の場合は、 **portableShell.bat** を起動し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングルールとスコアリングルールの自動更新を実行するには、スケジュールされたシステムタスクで次の同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linuxマシンへのインストール {#installing-on-a-linux-machine}

### Debianでのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用してPerlとSpamAssacinをインストールします。

   ```
   apt-get install spamassassin libxml-writer-perl
   ```

* serverConf.xml **ファイル** ( `/usr/local/[INSTALL]/nl6/conf/`で利用可能)で、spamCheck **行を次のよう** に変更します。

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

フィルタルールは、 **sa-updateツールを使用して自動的に更新できます** 。 詳しくは、公式のSpamAssacsin webサイトhttp://spamassassin.apache.org/ [を参照](http://spamassassin.apache.org/) してください。

Debianでは、更新は毎日自動的に行われます。

そうでない場合（例えば、Debianを手動でインストールした場合）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して **、このスクリプトを** crontabに挿入します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linuxでのパフォーマンスを向上させるには、/etc/spamassassin/local.cf **ファイルを編集し** 、ファイルの末尾に次の行を追加します。

```
dns_available no
```

