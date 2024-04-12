---
product: campaign
title: SpamAssassin の設定
description: SpamAssassin の設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 1f1004e2-dcd2-4ec5-98ec-720c205646d5
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# SpamAssassin の設定{#configuring-spamassassin}



>[!NOTE]
>
>一部の設定は、Adobeがホストするデプロイメントに対してのみAdobeが実行できます。 例えば、サーバーおよびインスタンス設定ファイルにアクセスするには、次の手順を実行します。 様々なデプロイメントの詳細については、 [ホスティングモデル](../../installation/using/hosting-models.md) セクションまたは宛先 [このページ](../../installation/using/capability-matrix.md).

## 概要 {#overview}

SpamAssassin は、望ましくないメールをフィルタリングするように設計されたソフトウェアの一部です。 Adobe Campaignは、このソフトウェアと連携してメールにスコアを割り当て、配信が開始される前にメッセージが望ましくないと見なされる可能性が高いかどうかを判断できます。 これを行うには、Adobe Campaignのアプリケーションサーバーに SpamAssassin をインストールして設定し、さらに一定数の Perl モジュールを使用する必要があります。

この章で説明する SpamAssassin のデプロイメントと統合は、デフォルトのソフトウェアインストールに基づいています。また、フィルタールールとスコアルールもデフォルトのソフトウェアインストールに基づいています。これらは、変更や最適化を加えずに SpamAssassin から提供されるルールです。 スコアアトリビューションとメッセージの選定は、SpamAssassin オプションの設定とフィルタリングルールにのみ基づいています。 ネットワーク管理者は、それらを会社のニーズに合わせる責任があります。

>[!IMPORTANT]
>
>SpamAssassin によって望ましくないものとしてメールが選定されるかどうかは、完全にフィルタリングおよびスコアルールに基づいています。
>
>したがって、SpamAssassin のインストールとAdobe Campaignへの統合が完全に機能し、送信前に配信に割り当てられたスコアの関連性を保証するには、これらのルールを 1 日に 1 回以上更新する必要があります。
>
>この更新は、SpamAssassin をホストするサーバー管理者の責任です。

Adobe Campaignでの SpamAssassin の使用は、Adobe Campaignから送信されるメールを受信した際に SpamAssassin を使用するメールサーバーの動作の可能性を示します。 ただし、インターネットプロバイダーやオンラインメールサーバーのメールサーバーが、Adobe Campaignから送信されるメッセージを依然として望ましくないと見なしている可能性があります。

Perl に SpamAssassin とそのモジュールをデプロイするには、HTTP 接続（TCP/80 フロー）経由でのインターネットアクセスを備えたAdobe Campaign アプリケーションサーバーが必要です。

## Windows マシンへのインストール {#installing-on-a-windows-machine}

Windows に SpamAssassin をインストールして設定し、Adobe Campaignとの統合を有効にするには、次の手順に従います。

1. SpamAssassin のインストール
1. Adobe Campaignへの SpamAssassin の統合

### SpamAssassin のインストール {#installing-spamassassin}

1. をに接続します [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) ユーザー資格情報を使用して。 ソフトウェア配布について詳しくは、を参照してください。 [このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja).
1. をダウンロード **Neolane Spam Assassin （Windows インストール）（2.0）** ファイル （neolane_spamassassin.2.0.zip）。
1. このファイルをAdobe Campaign サーバーにコピーしてから解凍します。

   >[!NOTE]
   >
   >パスが次の正規表現文字で構成されている場合は、必要な場所にファイルを解凍するように選択できます。 **`-_A-Za-z\xA0-\xFF0-9\.\%\@\=\+\,\/\\\:.`**. インストールパスに空白文字を含めることはできません。

1. ファイルを解凍したファイルに移動し、 **run_me.bat** インストールスクリプトを起動するファイル。

   Windows シェルが表示され、数秒間表示され続ける場合は、インストールと更新が完了するまで待ってから、 **Enter**.

   Windows シェルが表示されない、またはすぐに表示されなくなる前に表示されない場合は、次の手順に従い、 **portableShell.bat** ファイル：Windows シェルを表示し、シェルのパスがのフォルダーに対応していることを確認します **spamassassin.zip** ファイルは解凍されました。 これに該当しない場合は、 **cd** コマンド。

   Enter **run_me.bat** 次に、 **Enter** をクリックして、インストールと更新のプロセスを開始します。 操作は、更新の結果を示すために、次のいずれかの値を返します。

   * **0**：更新が実行されました。
   * **1**：利用できる新しい更新はありません。
   * **2**：利用可能な新しい更新プログラムはありません。
   * **3**：以前の検証中に更新に失敗しました。
   * **4** 以上：エラーが発生しました。

1. SpamAssassin のインストールが成功したことを確認するには、次の手順に従って GTUBE テスト（Generic Test for Unsolicited Bulk Email）を使用します。

   1. テキストファイルを作成して、の下に保存します。 **C:\TestSpamMail.txt**.
   1. 次の内容をファイルに挿入します。

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

   1. をダブルクリックします **portableShell.bat** ファイルを開いて Windows シェルを表示し、次のコマンド （または`<root>`」は、解凍時に作成したフォルダーを指定します  **spamassassin.zip** ファイル）:

      ```
       "<root>\perl\site\bin\spamassassin" "C:\TestSpamMail.txt"
      ```

      このテストメールのコンテンツは、SpamAssassin によって 1,000 ポイントスコアをトリガーします。 これは、望ましくないと検出され、インストールが成功し、完全に機能していることを意味します。

### Adobe Campaignへの SpamAssassin の統合 {#integrating-spamassassin-into-adobe-campaign}

1. を編集する **`[INSTALL]/conf/serverConf.xml`** ファイル。 で使用できるすべてのパラメーター **serverConf.xml** の一覧はこちら [セクション](../../installation/using/the-server-configuration-file.md).
1. の値を **spamCheck** 要素&#39; **コマンド** の属性 **Web** ノード。 これを行うには、次のコマンドを実行します。

   ```
   <spamCheck command='"<absolute path to the folder where you unzipped the zip file>\call_perl_with_args.bat" "<absolute path to nlserver>/spamcheck.pl"'/>
   ```

   >[!NOTE]
   >
   >すべてのパスは絶対パスである必要があります。

   を停止して開始する **[!UICONTROL Adobe Campaign]** サービス。

1. Adobe Campaignでの SpamAssassin の統合を確認するには、GTBUE テスト（未承諾のバルクメールの汎用テスト）を使用します。

   をダブルクリックします **portableshell.bat** ファイル。 これにより、Windows シェルの表示がトリガーされます。 次に、次のコマンドを実行します。

   ```
   perl "[INSTALL]\bin\spamcheck.pl" "C:\TestSpamMail.txt"
   ```

   このテストメールのコンテンツは、SpamAssassin によって割り当てられた 1,000 ポイントをトリガーします。 つまり、これは望ましくないと検出され、Adobe Campaignでの統合が成功し、完全に機能しています。

1. SpamAssassin フィルタリングおよびスコアルールの更新

   フィルタールールとスコアルールの初回の更新については、以下を開始してください **portableShell.bat** さらに、次のコマンドを実行します。

   ```
   sa-update --no-gpg
   ```

   フィルタールールとスコアルールの自動更新を実行するには、スケジュールされたシステムタスクで同じコマンドを使用します。

   ```
   sa-update --no-gpg
   ```

## Linux マシンへののインストール {#installing-on-a-linux-machine}

### Debian でのインストール手順 {#installation-steps-in-debian}

* 必要に応じて、次のコマンドを使用して Perl および SpamAssassin をインストールします。

  ```
  apt-get install spamassassin libxml-writer-perl
  ```

* が含まれる **serverConf.xml** ファイル （で利用可能） `/usr/local/[INSTALL]/nl6/conf/`）、を変更します。 **spamCheck** 行を次に示します。

  ```
  <spamCheck command="perl
  /usr/local/[NSTALL]/nl6/bin/spamcheck.pl"/>
  ```

### RHEL/CentOS のインストール手順 {#installation-steps-in-rhel-centos}

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

フィルタールールは、 **sa-update** ツール。 公式 SpamAssassin web サイトを参照してください。 [https://spamassassin.apache.org/](https://spamassassin.apache.org/) を参照してください。

Debian では、毎日自動的に更新が行われます。

これに該当しない場合（例えば、Debian を手動でインストールする場合）は、ルールの更新を自動化するスクリプトを作成します。

```
!/bin/sh
test -x /usr/bin/sa-update || exit 0
/usr/sbin/sa-update && /etc/init.d/spamassassin update
```

このスクリプトをに挿入 **crontab** 次のコマンドを使用：

```
crontab-e
```

### パフォーマンスの最適化 {#performance-optimization}

Linux のパフォーマンスを向上させるには、 **/etc/spamassassin/local.cf** ファイルを開き、ファイルの最後に次の行を追加します。

```
dns_available no
```
