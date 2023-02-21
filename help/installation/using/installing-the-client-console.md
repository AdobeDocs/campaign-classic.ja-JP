---
product: campaign
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法を説明します
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 7cc78214-92b8-4b1f-a307-96ec6af818d1
source-git-commit: 7f24c8be599d6dece41de848d64feb8079b10ff3
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 32%

---

# Campaign クライアントコンソールのインストールと更新{#installing-the-client-console}

![](../../assets/v7-only.svg)

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。

クライアントコンソールのインストールを開始する前に、次の操作を行う必要があります。

* お使いのシステムとツールについて、Adobe Campaign クライアントコンソールとの互換性を[互換性マトリックス](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)で確認してください。
* Campaign サーバーの URL を取得する
* ユーザー資格情報を取得する
* Microsoft Edge Webview2 ランタイムを (Campaign Classic7.3 のビルドバージョンから ) システムにインストールしておく。 [詳細情報](#webview)

クライアントコンソールをインストールまたは更新するプロセスは、Adobe Campaign Classicの実装によって異なります。
以下の詳細を確認して、実装に必要な事項を理解してください。

![](assets/do-not-localize/how-to-video.png) でAdobe Campaign Client をインストールしてセットアップする方法を説明します。 [ビデオ](#video)

>[!CAUTION]
>
>Campaign クライアントコンソールと Campaign アプリケーションサーバーは実行する必要があります **同じ製品バージョンで**. Adobeでは、 **同じ製品ビルド**. Campaign のクライアントとサーバーのバージョンを [この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version).

## Microsoft Edge WebView2 ランタイムのインストール {#webview}

Campaign Classic 7.3 ビルドバージョン以降、コンソールのインストールには Microsoft Edge WebView2 ランタイムのインストールが必要です。

WebView は、Windows 11 オペレーティングシステムの一部としてデフォルトでインストールされます。システム上にまだ存在しない場合は、Campaign Classicコンソールインストーラが、次の場所からダウンロードするように求めます。 [Microsoft Developer Web サイト](http://www.adobe.com/go/acc-ms-webview2-runtime-download_jp). Microsoft により Internet Explorer 11 ブラウザーのサポートが非推奨（廃止予定）となったので、Internet Explorer 11 ブラウザーではダウンロードリンクは機能しません。別のブラウザーを使用してリンクにアクセスしてください。

## Adobeがホストする実装 {#hosted-customers}

ホスト版のお客様には、クライアントコンソールをインストールまたは更新する 2 つのオプションがあります。

1. Adobeは、直接デプロイできます。 コンソールを更新すると、ポップアップウィンドウで最新のクライアントコンソールバージョンをダウンロードするように求められます。

1. からクライアントコンソールにダウンロードできます。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html)

   **ユーザーが更新を完了するには、管理者アクセス権が必要です。 ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールにデプロイする必要があります**

## ハイブリッドおよびオンプレミスの実装 {#hybrid-onprem-customers}

Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

### コンソールをユーザーが使用できるようにする {#make-console-available}

Adobe Campaignアプリケーションサーバー (nlserver web) の起動に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取った場合、Adobe Campaignリッチクライアントの設定プログラムをHTMLインターフェイスから使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動する際に、ユーザーに招待してダウンロードしてもらいます。

そのためには、次の手順を実行する必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、v7 の場合は setup-client-7.X.XXXX.exe、v6.1 の場合は setup-client-6.X.XXXX.exe と呼ばれます。X はAdobe Campaignのサブバージョン、XXXX はビルド番号です。

1. このパッケージを、（ハイブリッドインストールのマーケティングサーバーの）Adobe Campaignインストールフォルダーの/datakit/nl/eng/jsp の下にコピーして貼り付けます。

1. Adobe Campaignサーバーを起動します。


### 今後のこの質問オプションの使用を停止

Adobeは、オプションを終了することをお勧めします **[!UICONTROL 今後この質問をしない]** コンソールの新しいバージョンが利用可能になったときにすべてのユーザーに警告が表示されるようにするには、選択を解除します。  このオプションを選択すると、新しく利用可能になったバージョンは通知されません。

If **[!UICONTROL 今後この質問をしない]**  が選択されている場合は、このプロンプトをリセットできます。 以下の変更を行うのは、Windows レジストリの編集に慣れたシステム管理者のみです。

1. 次を使用してレジストリエディターを開く： **regedit** 命令 **[!UICONTROL スタート/実行]** メニュー

1. ノードを検索し、展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. を削除します。 **confAdvisedUpgrade** レジストリエディタを開き、閉じます。

>[!NOTE]
>
>既存の実装に更新されたコンソールを適用する場合、クライアントコンソールを更新するよう求めるプロンプトがユーザーに自動的に表示されます。 Campaign を初めて実装する場合は、ユーザーはコンソールをダウンロードする必要があります。 両方のオプションの詳細については、以下を参照してください

### 既存の実装のためのコンソールの更新{#update-the-client-console}

コンソールが Campaign サーバーフォルダーで使用可能になると、ポップアップウィンドウで最新のクライアントコンソールバージョンをダウンロードするよう求められます。

**ユーザーが更新を完了するには、管理者アクセス権が必要です。 ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールにデプロイする必要があります**


### 新しい実装用にコンソールをダウンロード{#download-the-client-console}

ユーザーは、次の手順に従ってコンソールをダウンロードし、インストールする必要があります。

1. Web ブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   `https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp` を参照してください。

1. ID ウィンドウで、ログインとパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成時に定義した内部アカウントの資格情報を使用します。

1. 次をクリック： **[!UICONTROL ダウンロード]** リンクをクリックします。
1. クライアントセットアップファイルをダウンロードして保存します。
1. Windows 上のコンピューターで、ダウンロードしたファイルを実行します。インストールが開始します。 クライアントコンソールのデフォルトのインストールパスは次のとおりです。 **$PROGRAMFILES$/Adobe/Adobe Campaign Classic vX クライアント**(「X」は「6」または「7」、Adobe Campaignのバージョンに応じて )

### 接続の作成 — 初めてのユーザーのみ{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. Windows からコンソールを起動します。 **[!UICONTROL 開始]** メニュー、 **Adobe Campaign** プログラムグループを作成します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプの URL を使用できます。

1. Adobe IMSが組織に対して設定されている場合は、「 」オプションをオンにします。 **[!UICONTROL Adobe IDとの接続]**

1. 「**[!UICONTROL OK]**」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼動環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

### Adobe Campaign へのログオン

既存のインスタンスにログオンするには、以下の手順に従います。

1. Windows からコンソールを起動します。 **[!UICONTROL 開始]** メニュー、 **Adobe Campaign** プログラムグループを作成します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要がある Campaign インスタンスを選択します。

1. クリック **[!UICONTROL Ok]**

1. ユーザーログイン資格情報を入力し、 **[!UICONTROL ログイン]**

>[!NOTE]
>
>Campaign Classic 7.3 ビルドバージョンでは、Adobe Campaign クライアントコンソールは、プロキシ認証中にプロキシ資格情報を 2 回要求する場合があります。これは、Internet Explorer とは異なり、Microsoft Edge WebView2 がプロキシ資格情報をキャッシュ／パスワードストアに保存しないためです。

**関連トピック**

* [インスタンスの作成とログイン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

## チュートリアルビデオ

このビデオでは、Adobe Campaign Client のインストールおよびセットアップ方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/35124?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
