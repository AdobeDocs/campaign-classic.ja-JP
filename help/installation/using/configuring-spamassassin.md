---
product: campaign
title: SpamAssassinの設定
description: SpamAssassinの設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 1f1004e2-dcd2-4ec5-98ec-720c205646d5
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 4%

---

# SpamAssassinの設定{#configuring-spamassassin}



>[!NOTE]
>
>一部の設定は、Adobeがホストするデプロイメントに対してのみAdobeで実行できます。 例えば、サーバーとインスタンスの設定ファイルにアクセスする場合などです。 様々なデプロイメントについて詳しくは、[&#x200B; ホスティングモデル &#x200B;](../../installation/using/hosting-models.md) セクションまたは[このページ &#x200B;](../../installation/using/capability-matrix.md)を参照してください。

## 概要 {#overview}

SpamAssassinは、望ましくない電子メールをフィルタリングするために設計されたソフトウェアの一部です。 このツールと連携することで、Adobe Campaignは電子メールにスコアを割り当て、配信を開始する前に、メッセージが望ましくないと見なされる可能性が高いかどうかを判断できます。 これを行うには、SpamAssassinをAdobe Campaignのアプリケーションサーバーにインストールして設定する必要があり、一定数のPerl モジュールを追加して動作させる必要があります。

この章で説明するSpamAssassinのデプロイメントと統合は、デフォルトのソフトウェアインストールに基づいています。また、フィルタリングとスコアリングルールも同様です。これらのルールは、SpamAssassinによって変更や最適化なしに提供されます。 スコアのアトリビューションとメッセージの選定は、SpamAssassin オプションの設定とフィルタリングルールのみに基づいています。 ネットワーク管理者は、自社のニーズに合わせてカスタマイズする責任があります。

>[!IMPORTANT]
>
>SpamAssassinによる望ましくないメールの選定は、フィルタリングとスコアリングのルールにもとづいています。
>
>したがって、SpamAssassinのインストールとAdobe Campaignへの統合が完全に機能し、送信する前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも1日1回更新する必要があります。
>
>このアップデートは、SpamAssassinをホストするサーバー管理者の責任です。

Adobe CampaignでSpamAssassinを使用すると、Adobe Campaignから送信されたメールを受信する際にSpamAssassinを使用するメールサーバーの動作の可能性を示します。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーは、Adobe Campaignが送信するメッセージを依然として望ましくないと考えている可能性があります。

SpamAssassinとそのモジュールをPerlにデプロイするには、HTTP接続（TCP/80 フロー）を介したインターネットアクセスを備えたAdobe Campaignアプリケーションサーバーが必要です。

## Windows マシンへのインストール {#installing-on-a-windows-machine}

WindowsでSpamAssassinをインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順を実行します。

1. SpamAssassinのインストール
1. SpamAssassinをAdobe Campaignに統合する

### SpamAssassinのインストール {#installing-spamassassin}

1. ユーザーの資格情報を使用して[&#x200B; ソフトウェア配布ポータル &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)に接続します。 ソフトウェア配布の詳細については、[このページ &#x200B;](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)を参照してください。
1. **Neolane Spam Assassin （Windows インストール） （2.0）** ファイル （neolane_spamassassin.2.0.zip）をダウンロードします。
1. このファイルをAdobe Campaign サーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字のいずれかで構成されている場合、必要に応じてファイルを展開できます：**`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**。 インストールパスに空白を含めることはできません。

1. ファイルを展開したファイルに移動し、**run_me.bat** ファイルをダブルクリックして、インストールスクリプトを起動します。

   Windows シェルが表示され、数秒間表示され続ける場合は、インストールと更新が完了するまで待ってから、**Enter**&#x200B;をクリックします。

   Windows シェルが表示されないか、すぐに消える前に表示されない場合は、次の手順に従って&#x200B;**portableShell.bat** ファイルをダブルクリックしてWindows シェルを表示し、**spamassassin.zip** ファイルが展開されているフォルダーにシェルパスが対応していることを確認します。 そうでない場合は、**cd** コマンドを使用してアクセスします。

   **run_me.bat**&#x200B;と入力し、**Enter**&#x200B;をクリックして、インストールと更新プロセスを開始します。 操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**：更新が実行されました。
   * **1**：利用可能な新しい更新はありません。
   * **2**：利用可能な新しい更新はありません。
   * **3**：以前の検証中に更新が失敗しました。
   * **4**&#x200B;以上：エラーが発生しました。

1. SpamAssassinのインストールが正常に完了したかどうかを確認するには、次の手順を使用してGTUBE テスト（未承諾の一括電子メールの汎用テスト）を使用します。

   1. テキストファイルを作成し、**C:\TestSpamMail.txt**&#x200B;に保存します。
   1. ファイルに次の内容を挿入します。

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

   1. **portableShell.bat** ファイルをダブルクリックしてWindows Shellを表示し、次のコマンドを起動します（**spamassassin.zip** ファイルを解凍する際に「`<root>`」が作成されたフォルダーを指定します）。

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテストメールの内容は、SpamAssassinの1,000 ポイントのスコアをトリガーしています。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssassinをAdobe Campaignに統合する {#integrating-spamassassin-into-adobe-campaign}

1. **`[INSTALL]/conf/serverConf.xml`** ファイルを編集します。 **serverConf.xml**&#x200B;で使用可能なすべてのパラメーターは、この[&#x200B; セクション &#x200B;](../../installation/using/the-server-configuration-file.md)に一覧表示されます。
1. **Web** ノードの&#x200B;**spamCheck**&#x200B;要素&#39; **command**&#x200B;属性の値を変更します。 これを行うには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   **[!UICONTROL Adobe Campaign]** サービスを停止して開始します。

1. Adobe CampaignでのSpamAssassinの統合を確認するには、GTBUE テスト（迷惑メールの汎用テスト）を使用します。

   **portableshell.bat** ファイルをダブルクリックします。 これにより、Windows シェルの表示がトリガーされます。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテストメールの内容は、SpamAssassinによって割り当てられた1,000 ポイントをトリガーしています。 これは、望ましくないと検出され、Adobe Campaignへの統合が成功し、完全に機能していることを意味します。

1. SpamAssassinのフィルタリングとスコアリングルールを更新する

   フィルタリングおよびスコアリングルールの最初の更新を行うには、**portableShell.bat**&#x200B;を起動し、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルターおよびスコアリングルールの自動更新を実行するには、スケジュールされたシステムタスクで同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linux マシンへのインストール {#installing-on-a-linux-machine}

### Debianのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用してPerlとSpamAssassinをインストールします。

  ```
  apt-get install spamassassin libxml-writer-perl
  ```

* **serverConf.xml** ファイル（`/usr/local/[INSTALL]/nl6/conf/`で使用可能）で、**spamCheck**&#x200B;行を次のように変更します。

  ```
  <spamCheck command="perl
  /usr/local/[NSTALL]/nl6/bin/spamcheck.pl"/>
  ```

### RHEL/CentOSのインストール手順 {#installation-steps-in-rhel-centos}

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

フィルタールールは、**sa-update** ツールを使用して自動的に更新できます。 詳しくは、SpamAssassinの公式web サイト [https://spamassassin.apache.org/](https://spamassassin.apache.org/)を参照してください。

Debianでは、更新は毎日自動的に行われます。

そうでない場合（例えばDebianが手動でインストールされている場合）、ルール更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

次のコマンドを使用して、このスクリプトを&#x200B;**crontab**&#x200B;に挿入します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linuxでのパフォーマンスを向上させるには、**/etc/spamassassin/local.cf** ファイルを編集し、ファイルの最後に次の行を追加します。

```
dns_available no
```
