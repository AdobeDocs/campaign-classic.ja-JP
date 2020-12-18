---
solution: Campaign Classic
product: campaign
title: SpamAssassin の設定
description: SpamAssassin の設定
audience: installation
content-type: reference
topic-tags: additional-configurations
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---


# SpamAssassin の設定{#configuring-spamassassin}

>[!NOTE]
>
>一部の設定は、Adobeがホストする配置に対してのみAdobeが実行できます。 例えば、サーバー設定ファイルやインスタンス設定ファイルにアクセスする場合です。 各デプロイメントの詳細については、[「モデルのホスト](../../installation/using/hosting-models.md)」セクションまたは[このページ](../../installation/using/capability-matrix.md)を参照してください。

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

## Windowsマシンにインストールする{#installing-on-a-windows-machine}

WindowsにSpamAssinをインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順を適用します。

1. SpamAssinのインストール
1. SpamAssinをAdobe Campaignに統合

### SpamAssin {#installing-spamassassin}をインストール中

1. ユーザーの資格情報を使用して、[ソフトウェア配布ポータル](https://experience.adobe.com/downloads)に接続します。 ソフトウェアの配布についての詳細は、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)を参照してください。
1. **Neolane Spam Assacin （Windowsのインストール） (2.0)**&#x200B;ファイル(neolane_spamassign.2.0.zip)をダウンロードします。
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規式文字のいずれかで構成されている場合は、必要に応じてファイルを解凍するように選択できます。**`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めることはできません。

1. ファイルの解凍先のファイルに移動し、重複が&#x200B;**run_me.bat**&#x200B;ファイルをクリックして、インストールスクリプトを起動します。

   Windowsシェルが表示され、数秒間表示され続ける場合は、インストールが完了して更新が終了するまで待ってから、**Enter**&#x200B;をクリックします。

   Windowsシェルが表示されない場合、または表示されない場合は、次の手順に従い、**portableShell.bat**&#x200B;ファイルを重複クリックしてWindowsシェルを表示し、シェルパスが&#x200B;**spamassin.zip**&#x200B;ファイルの解凍先のフォルダーに対応していることを確認します。 そうでない場合は、**cd**&#x200B;コマンドを使用してアクセスします。

   **run_me.bat**&#x200B;と入力し、**Enter**&#x200B;をクリックして、インストールと更新の処理を開始します。 この操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**:更新が行われました。
   * **1**:新しい更新プログラムはありません。
   * **2**:新しい更新プログラムはありません。
   * **3**:事前の検証中に更新に失敗しました。
   * **4** 以上：エラーが発生しました。

1. SpamAssinのインストールが正常に完了したことを確認するには、次の手順を使用してGTUBEテスト（非要請のバルク電子メール用の汎用テスト）を実行します。

   1. テキストファイルを作成し、**C:\TestSpamMail.txt**&#x200B;に保存します。
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

   1. **portableShell.bat**&#x200B;ファイルを重複がクリックすると、Windowsシェルが表示され、次のコマンドが起動します（または、**spamassin.zip**&#x200B;ファイルを解凍するときに、作成したフォルダーを指定します）。`<root>`

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト電子メールのコンテンツは、SpamAssicinによる1,000ポイントスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssicinをAdobe Campaignに統合{#integrating-spamassassin-into-adobe-campaign}

1. **`[INSTALL]/conf/serverConf.xml`**&#x200B;ファイルを編集します。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。
1. **Web**&#x200B;ノードの&#x200B;**spamCheck**&#x200B;要素&#39; **command**&#x200B;属性の値を変更します。 これを行うには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   **[!UICONTROL Adobe Campaign]**&#x200B;サービスを停止して開始します。

1. Adobe Campaign内のSpamAssinの統合を確認するには、GTBUEテスト（未請求のバルク電子メール用汎用テスト）を使用します。

   **portableshell.bat**&#x200B;ファイルを重複クリックします。 これにより、Windowsシェルの表示がトリガされます。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト電子メールのコンテンツは、SpamAssicinが割り当てた1,000ポイントをトリガーします。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. スパムアサシンのフィルタリングおよびスコアリングルールの更新

   フィルタリングとスコアリングルールの初期更新の場合は、開始&#x200B;**portableShell.bat**&#x200B;を実行し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングおよびスコアリング・ルールの自動更新を実行するには、スケジュールされたシステム・タスクで次の同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linuxマシンにインストールする{#installing-on-a-linux-machine}

### Debian {#installation-steps-in-debian}でのインストール手順

* 必要に応じて、次のコマンドを使用してPerlとSpamAssinをインストールします。

   ```
   apt-get install spamassassin libxml-writer-perl
   ```

* **serverConf.xml**&#x200B;ファイル（`/usr/local/[INSTALL]/nl6/conf/`から入手可能）で、**spamCheck**&#x200B;行を次のように変更します。

   ```
   <spamCheck command="perl
   /usr/local/[NSTALL]/nl6/bin/spamcheck.pl"/>
   ```

### RHEL/CentOS {#installation-steps-in-rhel-centos}でのインストール手順

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

### フィルター規則{#updating-filter-rules}を更新中

フィルタールールは、**sa-update**&#x200B;ツールを使用して自動的に更新できます。 詳しくは、公式のSpamAssinのWebサイト[http://spamassassin.apache.org/](http://spamassassin.apache.org/)を参照してください。

Debianでは、更新は毎日自動的に行われます。

そうでない場合（Debianが手動でインストールされている場合など）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して、**crontab**&#x200B;にこのスクリプトを挿入します。

```
crontab-e
```

### パフォーマンスの最適化{#performance-optimization}

Linuxでのパフォーマンスを向上させるには、**/etc/spamassassin/local.cf**&#x200B;ファイルを編集し、ファイルの末尾に次の行を追加します。

```
dns_available no
```

