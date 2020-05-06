---
title: SpamAssassin の設定
seo-title: SpamAssassin の設定
description: SpamAssassin の設定
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
source-git-commit: fcedad248169f53e716f2bd8b1b141fbf1f4d189
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---


# SpamAssassin の設定{#configuring-spamassassin}

>[!NOTE]
>
>一部の設定は、アドビがホストするデプロイメントに対してのみアドビが実行できます。 例えば、サーバー設定ファイルやインスタンス設定ファイルにアクセスする場合です。 各デプロイメントの詳細については、「 [ホスティングモデル](../../installation/using/hosting-models.md) 」の節または [この記事を参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-on-prem-vs-hosted.html)。

## 概要 {#overview}

SpamAssicinは、望ましくない電子メールをフィルターするように設計されたソフトウェアの一部です。 このソフトウェアと組み合わせて、Adobe Campaignは電子メールにスコアを割り当て、配信が起動される前にメッセージが望ましくないと見なされる可能性があるかどうかを判断できます。 これを行うには、SpamAssinをAdobe Campaignのアプリケーションサーバにインストールして設定する必要があります。また、Perlモジュールの動作には、一定の数の追加が必要です。

この章で説明するSpamAssinの展開と統合は、フィルタリングとスコアリングルールと同様、デフォルトのソフトウェアのインストールに基づいています。フィルタリングとスコアリングルールは、変更や最適化を行わずにSpamAssinが提供します。 スコアアトリビューションとメッセージの資格は、SpamAssinオプションの設定とフィルタールールのみに基づいています。 ネットワーク管理者は、会社のニーズに合わせてネットワークを調整する責任を負います。

>[!IMPORTANT]
>
>SpamAssicinが望ましくない電子メールの認定は、完全にフィルターとスコアリングルールに基づいています。
>
>したがって、SpamAssicinのインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日に1回更新する必要があります。
>
>この更新は、SpamAssinをホストするサーバー管理者の責任です。

SpamAssinをAdobe Campaignで使用すると、Adobe Campaignから送信された電子メールを受信したときにSpamAssinを使用するメールサーバーで発生する可能性がある動作を示します。 ただし、インターネットプロバイダやオンラインメールサーバのメールサーバは、Adobe Campaignから送信されるメッセージを望ましくないものと見なす可能性があります。

PerlにSpamAssinとそのモジュールを導入するには、HTTP接続（TCP/80フロー）を介したAdobe Campaignアクセスを備えたインターネットアプリケーションサーバーが必要です。

## Windowsマシンへのインストール {#installing-on-a-windows-machine}

WindowsにSpamAssinをインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順を適用します。

1. SpamAssinのインストール
1. SpamAssinをAdobe Campaignに統合

### SpamAssinのインストール {#installing-spamassassin}

1. ユーザーの資格情報を使用して [エクストラネットポータル](http://support.neolane.net) に接続します。
1. ダウンロードセンターに移動し **、ページを参照して「** ツール **** 」セクションを探します。
1. スパム **アサシン（Windowsのインストール）(1.0)** ファイルをダウンロードします。
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規式文字のいずれかで構成されている場合は、必要に応じてファイルを解凍するように選択できます。 **`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めることはできません。

1. ファイルの解凍先のファイルに移動し、重複が **run_me.bat** ファイルをクリックしてインストールスクリプトを起動します。

   Windowsシェルが表示され、数秒間表示され続ける場合は、インストールが完了して更新が終了するまで待ってから、 **Enterをクリックします**。

   Windowsシェルが表示されない場合、または表示されない場合は、次の手順に従い、 **portableShell.bat** ファイルを重複クリックしてWindowsシェルを表示し、Shellパスが、 **spamassin.zip** ファイルの解凍先のフォルダーに対応していることを確認します。 そうでない場合は、 **cd** コマンドを使用してアクセスします。

   「 **run_me.bat** 」と入力し、 **** Enterをクリックしてインストールと更新のプロセスを開始します。 この操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**: 更新が行われました。
   * **1**: 新しい更新プログラムはありません。
   * **2**: 新しい更新プログラムはありません。
   * **3**: 事前の検証中に更新に失敗しました。
   * **4** 以上： エラーが発生しました。

1. SpamAssinのインストールが正常に完了したことを確認するには、次の手順を使用してGTUBEテスト（非要請のバルク電子メール用の汎用テスト）を実行します。

   1. テキストファイルを作成し、C:\TestSpamMail.txtの下に保存し **ます**。
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

   1. portableShell.bat **ファイルを重複がクリックしてWindowsシェルを表示し、次のコマンドを起動します(または、「** 」は`<root>`spamassinin.zipファイルの解凍時に作成したフォルダーを指定します **** )。

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト電子メールのコンテンツは、SpamAssicinによる1,000ポイントスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssicinのAdobe Campaignへの統合 {#integrating-spamassassin-into-adobe-campaign}

1. ファイルを編集し **`[INSTALL]/conf/serverConf.xml`** ます。 serverConf.xmlで使用可能なすべてのパラメ **ーターをこの** 節に示します [](../../installation/using/the-server-configuration-file.md)。
1. **Web** ノードの **spamCheck** 要素の **** command属性の値を変更します。 これを行うには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   **[!UICONTROL Adobe Campaign]** サービスを停止して開始します。

1. Adobe Campaign内のSpamAssinの統合を確認するには、GTBUEテスト（未請求のバルク電子メール用汎用テスト）を使用します。

   portableshell.bat **ファイルを重複クリックします** 。 これにより、Windowsシェルの表示がトリガされます。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト電子メールのコンテンツは、SpamAssicinが割り当てた1,000ポイントをトリガーします。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. スパムアサシンのフィルタリングおよびスコアリングルールの更新

   フィルタリングとスコアリングルールの初期更新の場合は、開始 **portableShell.bat** を実行し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングおよびスコアリング・ルールの自動更新を実行するには、スケジュールされたシステム・タスクで次の同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linuxマシンへのインストール {#installing-on-a-linux-machine}

### Debianでのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用してPerlとSpamAssinをインストールします。

   ```
   apt-get install spamassassin libxml-writer-perl
   ```

* serverConf.xml **ファイル(** )で `/usr/local/[INSTALL]/nl6/conf/`、spamCheck **** 行を次のように変更します。

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

フィルタルールは、 **sa-update** ツールを使用して自動的に更新できます。 詳しくは、公式のSpamAssicin Webサイトhttp://spamassassin.apache.org/ [を参照してください](http://spamassassin.apache.org/) 。

Debianでは、更新は毎日自動的に行われます。

そうでない場合（Debianが手動でインストールされている場合など）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して、 **crontab** にこのスクリプトを挿入します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linuxでのパフォーマンスを向上させるには、/etc/spamassassin/local.cf **** ファイルを編集し、ファイルの末尾に次の行を追加します。

```
dns_available no
```

