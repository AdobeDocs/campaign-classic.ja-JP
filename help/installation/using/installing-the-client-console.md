---
solution: Campaign Classic
product: campaign
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 7cc78214-92b8-4b1f-a307-96ec6af818d1
translation-type: tm+mt
source-git-commit: 2ce19e135ce1eb47d760c5407446312bc2d3c303
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 6%

---

# キャンペーンクライアントコンソールのインストールと更新{#installing-the-client-console}

キャンペーンクライアントコンソールは、キャンペーンアプリケーションサーバーに接続できるリッチクライアントです。

クライアントコンソールのインストールを開始する前に、次の操作を行う必要があります。

* [互換表](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)のAdobe Campaignとの互換性を確認してください
* キャンペーンサーバーのURLを取得する
* ユーザー資格情報の取得

クライアントコンソールをインストールまたは更新するプロセスは、Adobe Campaign Classicの導入環境によって異なります。
以下の詳細を確認し、導入に必要なものを確認してください。

![](assets/do-not-localize/how-to-video.png) ビデオでのAdobe Campaignクライアントのインストールおよびセットアップ方法の確認 [](#video)

>[!CAUTION]
>
>キャンペーンクライアントコンソールとキャンペーンアプリケーションサーバーは、同じ製品バージョン&#x200B;**で**&#x200B;実行する必要があります。 また、Adobeでは&#x200B;**同じ製品ビルド**&#x200B;を使用することを強くお勧めします。 [このセクション](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、キャンペーンクライアントとサーバーのバージョンを確認する方法を説明します。

## Adobeがホストする実装{#hosted-customers}

ホストされる顧客に対しては、クライアントコンソールをインストールまたは更新する方法が2つあります。

1. Adobeは直接デプロイできます。 コンソールが更新されると、ポップアップウィンドウで最新のクライアントコンソールバージョンをダウンロードするように求められます。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)からクライアントコンソールにダウンロードできます

   **更新を完了するには、管理者アクセス権が必要です。ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールに展開する必要があります**

## ハイブリッドおよびオンプレミス導入{#hybrid-onprem-customers}

作成および設定したインスタンスにログオンできるAdobe Campaignユーザーには、クライアントコンソールを使用する必要があります。

### コンソールをユーザーが利用できるようにする{#make-console-available}

Adobe Campaignアプリケーションサーバー(nlserver Web)の開始に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取る場合、HTMLインターフェイスを介してAdobe Campaignリッチクライアントのセットアッププログラムを使用できるように設定できます。 クライアントコンソールの新しいバージョンが利用可能になった場合は、ユーザーはクライアントコンソールを起動する際に、ダウンロードするよう招待されます。

これを行うには、次の操作を行う必要があります。

1. コンソールのインストールプログラムを含むパッケージを選択します。

   このファイルは、v7の場合はsetup-client-7.X.XXXX.exe、v6.1の場合はsetup-client-6.X.XXXX.exeと呼ばれます。XはAdobe Campaignのサブバージョン、XXXXはビルドです   number.

1. このパッケージを/datakit/nl/eng/jspの下のAdobe Campaignーインストールフォルダー（ハイブリッドインストールの場合はマーケティングサーバー）にコピー&amp;ペーストします。

1. 開始Adobe Campaignサーバー。


### この質問オプションを表示しない

Adobeでは、**[!UICONTROL 「この質問]**&#x200B;は選択しないでください」オプションを選択し、コンソールの新しいバージョンが利用可能な場合にすべてのユーザーに警告が表示されるようにすることをお勧めします。  このオプションを選択すると、新しい利用可能なバージョンは通知されません。

**[!UICONTROL この質問]**&#x200B;が選択されている場合は、このプロンプトをリセットできます。 次の変更を行うのは、Windowsレジストリの編集に慣れたシステム管理者のみです。

1. **[!UICONTROL 開始/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリエディターを開きます。

1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade**&#x200B;エントリを削除し、レジストリエディターを閉じます。

>[!NOTE]
>
>既存の実装に更新されたコンソールを適用する場合、ユーザーは、クライアントコンソールを更新するように求めるプロンプトを自動的に受け取ります。 キャンペーンを初めて導入する場合は、コンソールをダウンロードする必要があります。 両方のオプションの詳細については、以下を参照してください。

### 既存の実装に合わせてコンソールを更新{#update-the-client-console}

コンソールがキャンペーンサーバーフォルダーで使用可能になると、ポップアップウィンドウで最新のクライアントコンソールバージョンをダウンロードするように求められます。

**更新を完了するには、管理者アクセス権が必要です。ユーザーに管理者権限がない場合、システム管理者はすべてのクライアントコンソールに展開する必要があります**


### 新しい導入用にコンソールをダウンロード{#download-the-client-console}

次の手順に従って、コンソールをダウンロードしてインストールする必要があります。

1. Webブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   [`https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp`](https://myserver.adobe.com/nl/jsp/logon.jsp).

1. IDウィンドウで、ログイン名とパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成時に定義した内部アカウントの資格情報を使用します。

1. インストールページの&#x200B;**[!UICONTROL ダウンロード]**&#x200B;リンクをクリックします。
1. クライアントセットアップファイルをダウンロードして保存します。
1. Windowsのコンピューターで、ダウンロードしたファイルを実行します。インストール開始がアップになります。 クライアントコンソールのデフォルトのインストールパスは、Adobe Campaignのバージョンに応じて、**$PROGRAMFILES$/Adobe/Adobe Campaign ClassicvXクライアント**&#x200B;です。「X」は「6」または「7」です。

### 接続の作成 — 初回ユーザーのみ{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. **Adobe Campaign**&#x200B;プログラムグループのWindows **[!UICONTROL 開始]**&#x200B;メニューからコンソールを開始します。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加/Connection]**&#x200B;をクリックし、Adobe CampaignアプリケーションサーバーのラベルとURLを入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URLを介したAdobe Campaignアプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、またはIPアドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com)タイプURLを使用できます。

1. AdobeIMSが組織に対して設定されている場合は、「**[!UICONTROL Adobe ID]**&#x200B;に接続する」オプションを選択します

1. 「**[!UICONTROL OK]**」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼働環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

### Adobe Campaignへのログオン

既存のインスタンスにログオンするには、次の手順に従います。

1. **Adobe Campaign**&#x200B;プログラムグループのWindows **[!UICONTROL 開始]**&#x200B;メニューからコンソールを開始します。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要があるキャンペーンインスタンスを選択します。

1. 「**[!UICONTROL OK]**」をクリックします

1. ユーザーログイン資格情報を入力し、「**[!UICONTROL ログイン]**」をクリックします。


**関連トピック**

* [インスタンスの作成とログイン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

## チュートリアルビデオ

このビデオでは、Adobe Campaignクライアントのインストールとセットアップの方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/35124?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.ad?lang=obe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
