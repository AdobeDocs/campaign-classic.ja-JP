---
product: campaign
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法を説明します
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 7cc78214-92b8-4b1f-a307-96ec6af818d1
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 23%

---

# Campaignクライアントコンソールのインストールと更新{#installing-the-client-console}

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。

クライアントコンソールのインストールを開始する前に、次の操作を行う必要があります。

* [互換性マトリックス](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)のAdobe Campaignとのシステムおよびツールの互換性を確認してください
* CampaignサーバーURLの取得
* ユーザー資格情報の取得

クライアントコンソールをインストールまたは更新するプロセスは、Adobe Campaign Classicの実装によって異なります。
実装に必要な事項については、以下の詳細を確認してください。

![](assets/do-not-localize/how-to-video.png) ビデオでAdobe Campaign Clientのインストールとセットアップ方法を確認 [する](#video)

>[!CAUTION]
>
>CampaignクライアントコンソールとCampaignアプリケーションサーバーは、同じ製品バージョン&#x200B;**で**&#x200B;を実行する必要があります。 Adobeは、**同じ製品ビルド**&#x200B;を使用することを強くお勧めします。 [この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)でCampaignクライアントとサーバーのバージョンを確認する方法を説明します。

## Adobeホスト実装{#hosted-customers}

ホスト型の顧客に対しては、クライアントコンソールをインストールまたは更新する方法が2つあります。

1. Adobeは、直接デプロイできます。 コンソールが更新されると、最新のクライアントコンソールバージョンをポップアップウィンドウでダウンロードするように求められます。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)からクライアントコンソールにダウンロードできます。

   **更新を完了するには、管理者アクセス権が必要です。ユーザーに管理者権限がない場合、システム管理者は、すべてのクライアントコンソールに**&#x200B;をデプロイする必要があります。

## ハイブリッドおよびオンプレミス実装{#hybrid-onprem-customers}

Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

### コンソールをユーザーが使用できるようにする{#make-console-available}

Adobe Campaignアプリケーションサーバー(nlserver web)の起動に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取ったら、Adobe CampaignリッチクライアントのセットアッププログラムをHTMLインターフェイスを介して使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動すると、そのコンソールをダウンロードするようにユーザーが招待されます。

これをおこなうには、次の操作を行う必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、v7の場合はsetup-client-7.X.XXXX.exe、v6.1の場合はsetup-client-6.X.XXXX.exeと呼ばれます。ここで、XはAdobe Campaignのサブバージョン、XXXXはビルドです。   数値

1. このパッケージを、 /datakit/nl/eng/jspの下のAdobe Campaignインストールフォルダー（ハイブリッドインストールの場合はマーケティングサーバー上）にコピーして貼り付けます。

1. Adobe Campaignサーバーを起動します。


### 今後の質問オプション

Adobeは、「**[!UICONTROL この質問]**&#x200B;は選択しないでください」オプションを選択し、新しいバージョンのコンソールが利用可能になったときにすべてのユーザーに警告が表示されるようにすることをお勧めします。  このオプションを選択すると、新しく利用可能になったバージョンは通知されません。

「**[!UICONTROL この質問を表示しない]**」が選択されている場合は、このプロンプトをリセットできます。 以下の変更は、Windowsレジストリの編集に慣れたシステム管理者のみが行う必要があります。

1. **[!UICONTROL スタート/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリエディターを開きます。

1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade**&#x200B;エントリを削除し、レジストリエディターを閉じます。

>[!NOTE]
>
>既存の実装に更新されたコンソールを適用する場合、クライアントコンソールを更新するよう求めるプロンプトがユーザーに自動的に表示されます。 初めてCampaignを実装する場合は、ユーザーはコンソールをダウンロードする必要があります。 両方のオプションの詳細については、以下を参照してください

### 既存の実装のコンソールを更新します。{#update-the-client-console}

コンソールがCampaignサーバーフォルダーで使用可能になると、最新のクライアントコンソールバージョンをポップアップウィンドウでダウンロードするよう求めるプロンプトが表示されます。

**ユーザーが更新を完了するには、管理者アクセス権が必要です。ユーザーに管理者権限がない場合、システム管理者は、すべてのクライアントコンソールに**&#x200B;をデプロイする必要があります。


### 新しい実装用にコンソールをダウンロードします。{#download-the-client-console}

次の手順に従って、コンソールをダウンロードしてインストールする必要があります。

1. Webブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   [`https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp`](https://myserver.adobe.com/nl/jsp/logon.jsp).

1. 識別ウィンドウで、ログイン名とパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成中に定義された内部アカウントの資格情報を使用します。

1. インストールページの「**[!UICONTROL ダウンロード]**」リンクをクリックします。
1. クライアント設定ファイルをダウンロードして保存します。
1. Windows上のコンピューターでダウンロードしたファイルを実行します。インストールが開始します。 クライアントコンソールのデフォルトのインストールパスは&#x200B;**$PROGRAMFILES$/Adobe/Adobe Campaign Classic vXクライアント**&#x200B;です。「X」はAdobe Campaignのバージョンに応じて「6」または「7」です。

### 接続を作成します。初めてユーザーのみ{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. **Adobe Campaign**&#x200B;プログラムグループのWindowsの&#x200B;**[!UICONTROL 開始]**&#x200B;メニューからコンソールを起動します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプの URL を使用できます。

1. AdobeIMSが組織に対して設定されている場合は、「**[!UICONTROL Adobe IDに接続]**」オプションをオンにします。

1. 「**[!UICONTROL OK]**」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼動環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

### Adobe Campaign へのログオン

既存のインスタンスにログオンするには、以下の手順に従います。

1. **Adobe Campaign**&#x200B;プログラムグループのWindowsの&#x200B;**[!UICONTROL 開始]**&#x200B;メニューからコンソールを起動します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要がある Campaign インスタンスを選択します。

1. 「**[!UICONTROL OK]**」をクリックします。

1. ユーザーログイン資格情報を入力し、「**[!UICONTROL ログイン]**」をクリックします。


**関連トピック**

* [インスタンスの作成とログイン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

## チュートリアルビデオ

このビデオでは、Adobe Campaign Clientのインストールおよび設定方法を示します。

>[!VIDEO](https://video.tv.adobe.com/v/35124?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.ad?lang=obe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
