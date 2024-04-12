---
product: campaign
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法を学ぶ
feature: Installation, Upgrade
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 7cc78214-92b8-4b1f-a307-96ec6af818d1
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 31%

---

# Campaign クライアントコンソールのインストールと更新{#installing-the-client-console}

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。

クライアントコンソールのインストールを開始する前に、次の操作をおこなう必要があります。

* お使いのシステムとツールについて、Adobe Campaign クライアントコンソールとの互換性を[互換性マトリックス](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)で確認してください。
* Campaign サーバーの URL を取得する
* ユーザー資格情報を取得する
* Microsft Edge Webview2 ランタイムをシステムにインストールします（Campaign Classic 7.3 のビルドバージョンから）。 [詳細情報](#webview)

クライアントコンソールをインストールまたは更新するプロセスは、Adobe Campaign Classicの実装によって異なります。
実装に必要な事項を理解するには、以下の詳細を確認してください。

![](assets/do-not-localize/how-to-video.png) でAdobe Campaign クライアントをインストールおよび設定する方法を確認してください [ビデオ](#video)

>[!CAUTION]
>
>* Campaign クライアントコンソールと Campaign アプリケーションサーバーを実行する必要がある **同じ製品バージョンで**. Adobeは、を使用することを強くお勧めします **同じ製品ビルド**. で Campaign クライアントとサーバーのバージョンを確認する方法を学ぶ [この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version).
>
>* コンソールがインストールされているインストールフォルダーへのアクセスは、意図したユーザーのみに制限してください。これにより、書き込み権限が適切に制限されます。



## Microsoft Edge WebView2 ランタイムのインストール {#webview}

Campaign Classic 7.3 ビルドバージョン以降、コンソールのインストールには Microsoft Edge WebView2 ランタイムのインストールが必要です。

WebView は、Windows 11 オペレーティングシステムの一部としてデフォルトでインストールされます。システムにまだインストールされていない場合、Campaign Classicコンソールインストーラーにより、次からダウンロードするように求められます。 [Microsoft開発者向け web サイト](https://www.adobe.com/go/acc-ms-webview2-runtime-download_jp). Microsoft により Internet Explorer 11 ブラウザーのサポートが非推奨（廃止予定）となったので、Internet Explorer 11 ブラウザーではダウンロードリンクは機能しません。別のブラウザーを使用してリンクにアクセスしてください。

## Adobeホスト型実装 {#hosted-customers}

ホステッド環境のお客様は、クライアントコンソールをインストールまたは更新するために、次の 2 つのオプションがあります。

1. Adobeは直接デプロイできます。 コンソールが更新されると、ポップアップウィンドウで最新のクライアントコンソールバージョンをダウンロードするように求められます。

1. クライアントコンソールには、 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)

   **ユーザーが更新を完了するには、管理者アクセス権が必要です。 ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールにをデプロイする必要があります**

## ハイブリッド実装およびオンプレミス実装 {#hybrid-onprem-customers}

Adobe Campaign ユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

### ユーザーによるコンソールの利用 {#make-console-available}

Adobe Campaign アプリケーションサーバー（nlserver web）の起動に使用するコンピューターがクライアントコンソールからユーザー接続を受け取ると、そのコンピューターを設定することにより、Adobe Campaign リッチクライアント用の設定プログラムをHTMLインターフェイスで使用できるようになります。 クライアントコンソールの新しいバージョンが利用可能になると、クライアントコンソールの起動時にユーザーがクライアントコンソールをダウンロードするように招待されます。

そのためには、次の手順を実行する必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、setup-client-7.X.XXXX.exe と呼ばれます。ここで、X はAdobe Campaignのサブバージョンで、XXXX はビルド番号です。

1. このパッケージをコピーして、/datakit/nl/eng/jsp の下のAdobe Campaign インストールフォルダー（ハイブリッドインストールの場合は marketing server 上）に貼り付けます。

1. Adobe Campaign サーバーを起動します。


### 今後この質問をしないオプション

Adobeは、このオプションを使用しないことをお勧めします **[!UICONTROL 今後この質問をしない]** コンソールの新しいバージョンが利用可能になったときに、すべてのユーザーにアラートが送信されるようにするには、このオプションを選択しないでください。  このオプションを選択すると、新しく利用可能になったバージョンは通知されません。

次の場合 **[!UICONTROL 今後この質問をしない]**  が選択されました。このプロンプトをリセットできます。 Windows レジストリの編集に慣れているシステム管理者だけが、次の変更を行う必要があります。

1. を使用してレジストリエディターを開きます。 **regedit** コマンドを **[!UICONTROL 開始/実行]** メニュー。

1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. を削除 **confAdvisedUpgrade** レジストリ エディタを開いて閉じます。

>[!NOTE]
>
>更新されたコンソールを既存の実装に適用する場合、クライアントコンソールを更新するように求めるプロンプトがユーザーに自動的に表示されます。 Campaign を初めて実装する場合は、コンソールをダウンロードする必要があります。 両方のオプションについて詳しくは、こちらを参照してください

### 既存の実装のコンソールの更新{#update-the-client-console}

Campaign サーバーフォルダーでコンソールを使用できるようになると、ポップアップウィンドウに最新のクライアントコンソールバージョンをダウンロードするように求められます。

**ユーザーが更新を完了するには、管理者アクセス権が必要です。 ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールにをデプロイする必要があります**


### 新しい実装のためのコンソールのダウンロード{#download-the-client-console}

ユーザーは、次の手順に従って、コンソールをダウンロードしてインストールする必要があります。

1. Web ブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   `https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp` を参照してください。

1. ID ウィンドウに、ログインとパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成時に定義した内部アカウントの資格情報を使用します。

1. 「」をクリックします **[!UICONTROL Download]** インストールページのリンク。
1. クライアント設定ファイルをダウンロードして保存します。
1. ダウンロードしたファイルを Windows のコンピューターで実行します。インストールが開始されます。 クライアントコンソールのデフォルトのインストールパスはです。 **$PROGRAMFILES$/Adobe/Adobe Campaign Classic vX クライアント**：ここで「X」は、Adobe Campaignのバージョンに応じて「6」または「7」です。

### 接続の作成 – 初回ユーザーのみ{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. Windows からコンソールを起動します **[!UICONTROL 開始]** メニュー（内） **Adobe Campaign** プログラムグループ。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、 `https://<machine>.<domain>.com` url を入力します。

1. Adobe IMSが組織に対して設定されている場合は、「」オプションをオンにします **[!UICONTROL Adobe IDとの接続]**

1. 「**[!UICONTROL OK]**」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼動環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

### Adobe Campaign へのログオン

既存のインスタンスにログオンするには、以下の手順に従います。

1. Windows からコンソールを起動します **[!UICONTROL 開始]** メニュー（内） **Adobe Campaign** プログラムグループ。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要がある Campaign インスタンスを選択します。

1. クリック **[!UICONTROL Ok]**

1. ユーザーログイン資格情報を入力し、 **[!UICONTROL ログイン]**

>[!NOTE]
>
>Campaign Classic 7.3 ビルドバージョンでは、Adobe Campaign クライアントコンソールは、プロキシ認証中にプロキシ資格情報を 2 回要求する場合があります。これは、Internet Explorer とは異なり、Microsoft Edge WebView2 がプロキシ資格情報をキャッシュ／パスワードストアに保存しないためです。

**関連トピック**

* [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

## チュートリアルビデオ

このビデオでは、Adobe Campaign クライアントをインストールおよびセットアップする方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/35124?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
