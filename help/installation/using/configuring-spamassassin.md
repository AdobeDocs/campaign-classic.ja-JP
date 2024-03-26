---
product: campaign
title: SpamAssassin の設定
description: SpamAssassin の設定
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 1f1004e2-dcd2-4ec5-98ec-720c205646d5
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 2%

---

# SpamAssassin の設定{#configuring-spamassassin}



>[!NOTE]
>
>一部の設定は、Adobeがホストするデプロイメントの場合、Adobeが実行できるだけです。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合です。 様々なデプロイメントについて詳しくは、 [ホスティングのモデル](../../installation/using/hosting-models.md) セクションまたは [このページ](../../installation/using/capability-matrix.md).

## 概要 {#overview}

SpamAssassin は、望ましくない E メールをフィルタリングするように設計されたソフトウェアです。 Adobe Campaignは、このソフトウェアと組み合わせて、E メールにスコアを割り当て、配信が開始される前にメッセージが望ましくないと見なされる可能性があるかどうかを判断できます。 これをおこなうには、SpamAssassin をAdobe Campaignのアプリケーションサーバーにインストールして設定し、一定数の追加の Perl モジュールを動作させる必要があります。

この章で説明する SpamAssassin のデプロイと統合は、SpamAssassin が提供するフィルタリングとスコアリングルールと同様、デフォルトのソフトウェアインストールに基づいています。変更や最適化はおこなわれません。 スコアのアトリビューションとメッセージの選定は、SpamAssassin オプションの設定とフィルタリングルールにのみ基づいています。 ネットワーク管理者は、自社のニーズに合わせてネットワーク管理者を配置します。

>[!IMPORTANT]
>
>SpamAssassin によって望ましくない電子メールの選定は、完全にフィルタリングとスコア付けルールに基づいています。
>
>したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するために、これらのルールを少なくとも 1 日に 1 回更新する必要があります。
>
>この更新は、SpamAssassin をホストするサーバー管理者の責任です。

Adobe Campaignでの SpamAssassin の使用は、Adobe Campaignから送信された E メールを受信したときに SpamAssassin を使用するメールサーバーが起こりうる動作を示します。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーでは、Adobe Campaignから送信されるメッセージが引き続き望ましくないと見なされる可能性があります。

SpamAssassin とそのモジュールを Perl にデプロイするには、HTTP 接続（TCP/80 フロー）を介したインターネットアクセスを備えたAdobe Campaignアプリケーションサーバーが必要です。

## Windows マシンへのインストール {#installing-on-a-windows-machine}

Windows に SpamAssassin をインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順に従います。

1. SpamAssassin のインストール
1. SpamAssassin をAdobe Campaignに統合

### SpamAssassin のインストール {#installing-spamassassin}

1. 次に接続： [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) ユーザー資格情報を使用して。 ソフトウェア配布について詳しくは、 [このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja).
1. をダウンロードします。 **Neolane Spam Assassin（Windows インストール）(2.0)** ファイル (neolane_spamassassin.2.0.zip)
1. このファイルをAdobe Campaignサーバーにコピーし、解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字のいずれかで構成されている場合は、必要な場所にファイルを解凍するように選択できます。 **`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めることはできません。

1. ファイルを解凍したファイルに移動し、 **run_me.bat** ファイルを使用して、インストールスクリプトを起動します。

   Windows シェルが表示され、数秒間表示され続ける場合は、インストールが完了して更新が完了するまで待ってから、[ ] をクリックします。 **入力**.

   Windows シェルが表示されない場合、または表示されない場合は、次の手順に従い、 **portableShell.bat** Windows シェルを表示するファイルと、シェルパスが **spamassassin.zip** ファイルが解凍されました。 該当しない場合は、 **cd** コマンドを使用します。

   入力 **run_me.bat** 次に、「 **入力** をクリックして、インストールと更新のプロセスを開始します。 この操作では、更新の結果を示すために、次のいずれかの値が返されます。

   * **0**：更新が実行されました。
   * **1**：新しい更新はありません。
   * **2**：新しい更新はありません。
   * **3**：前の検証中に更新に失敗しました。
   * **4** またはその他：エラーが発生しました。

1. SpamAssassin のインストールが成功したかどうかを確認するには、次の手順に従って、GTUBE テスト（未承諾の一括電子メール用汎用テスト）を使用します。

   1. テキストファイルを作成し、以下に保存します。 **C:\TestSpamMail.txt**.
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

   1. をダブルクリックします。 **portableShell.bat** ファイルを開き、Windows シェルを表示し、次のコマンド ( または「`<root>`「 」は、  **spamassassin.zip** ファイル ):

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテスト E メールのコンテンツは、SpamAssassin による 1,000 ポイントのスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### SpamAssassin のAdobe Campaignへの統合 {#integrating-spamassassin-into-adobe-campaign}

1. を編集します。 **`[INSTALL]/conf/serverConf.xml`** ファイル。 次の **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).
1. 値を **spamCheck** 要素 **command** 属性 **Web** ノード。 これをおこなうには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   を停止して起動します。 **[!UICONTROL Adobe Campaign]** サービス。

1. Adobe Campaignで SpamAssassin の統合を確認するには、GTBUE テスト（未承諾のバルクメール用 Generic Test）を使用します。

   をダブルクリックします。 **portableshell.bat** ファイル。 このトリガーは、Windows シェルの表示です。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテスト用 E メールのコンテンツは、SpamAssassin によってトリガーされた 1,000 ポイントを割り当てました。 これは、望ましくないと検出され、Adobe Campaignの統合が成功し、完全に機能していることを意味します。

1. SpamAssassin のフィルタリングとスコア付けルールを更新

   フィルターとスコア付けルールの初期更新の場合は、まず **portableShell.bat** 次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタリングルールとスコアリングルールの自動更新を実行するには、スケジュールされたシステムタスクで次の同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linux マシンへのインストール {#installing-on-a-linux-machine}

### Debian でのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用して Perl および SpamAssassin をインストールします。

  ```
  apt-get install spamassassin libxml-writer-perl
  ```

* Adobe Analytics の **serverConf.xml** ファイル ( `/usr/local/[INSTALL]/nl6/conf/`)、 **spamCheck** 行を次に示します。

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

### フィルタールールを更新中 {#updating-filter-rules}

フィルタールールは、 **sa-update** ツールを使用します。 SpamAssassin の公式 Web サイトを参照してください。 [https://spamassassin.apache.org/](https://spamassassin.apache.org/) を参照してください。

Debian では、更新は毎日自動的におこなわれます。

そうでない場合（Debian を手動でインストールする場合など）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

このスクリプトを次に挿入： **crontab** 次のコマンドを使用します。

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linux のパフォーマンスを向上させるには、 **/etc/spamassassin/local.cf** ファイルの最後に次の行を追加します。

```
dns_available no
```
