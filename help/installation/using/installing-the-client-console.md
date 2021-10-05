---
product: campaign
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法を説明します
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 7cc78214-92b8-4b1f-a307-96ec6af818d1
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 25%

---

# Campaign クライアントコンソールのインストールと更新{#installing-the-client-console}

![](../../assets/v7-only.svg)

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。

クライアントコンソールのインストールを開始する前に、次の操作を行う必要があります。

* お使いのシステムとツールについて、Adobe Campaign クライアントコンソールとの互換性を[互換性マトリックス](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)で確認してください。
* Campaign サーバーの URL を取得する
* ユーザー資格情報を取得する

クライアントコンソールをインストールまたは更新するプロセスは、Adobe Campaign Classicの実装によって異なります。
実装に必要な情報については、以下の詳細を確認してください。

![](assets/do-not-localize/how-to-video.png) ビデオでAdobe Campaign Client のインストールとセットアップの [方法](#video)

>[!CAUTION]
>
>Campaign クライアントコンソールと Campaign アプリケーションサーバーは、同じ製品バージョン **で** 実行する必要があります。 Adobeは、**同じ製品ビルド** を使用することを強くお勧めします。 Campaign クライアントとサーバーのバージョンを確認する方法については、[ この節 ](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version) を参照してください。

## Adobeがホストする実装 {#hosted-customers}

ホスト型の顧客に対しては、次の 2 つの方法でクライアントコンソールをインストールまたは更新できます。

1. Adobeは、直接デプロイできます。 コンソールを更新すると、最新のクライアントコンソールバージョンをポップアップウィンドウでダウンロードするように求められます。

1. [ ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html) からクライアントコンソールにダウンロードできます。

   **更新を完了するには、管理者アクセス権が必要です。ユーザーが管理者権限を持っていない場合、システム管理者はすべてのクライアントコンソールにデプロイする必要があります**

## ハイブリッドおよびオンプレミスの実装 {#hybrid-onprem-customers}

Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

### コンソールをユーザーが使用できるようにする {#make-console-available}

Adobe Campaignアプリケーションサーバー (nlserver web) の起動に使用するコンピューターがクライアントコンソールからユーザー接続を受け取った場合、Adobe Campaignのリッチクライアントのセットアッププログラムを HTML インターフェイスを介して使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動すると、そのコンソールをダウンロードするように招待されます。

これをおこなうには、次の操作をおこなう必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、v7 の場合は setup-client-7.X.XXXX.exe、v6.1 の場合は setup-client-6.X.XXXX.exe と呼ばれます。ここで、X はAdobe Campaignのサブバージョンで、XXX はビルドです。   数値

1. このパッケージを、（ハイブリッドインストールの場合はマーケティングサーバーの）Adobe Campaignインストールフォルダーの/datakit/nl/eng/jsp の下にコピーして貼り付けます。

1. Adobe Campaignサーバーを起動します。


### 今後のこの質問オプションの使用

Adobeは、「**[!UICONTROL この質問]** は選択しないでください」オプションを選択したままにして、新しいバージョンのコンソールが利用可能になったときにすべてのユーザーに警告が表示されるようにすることをお勧めします。  このオプションを選択すると、新しく利用可能になったバージョンは通知されません。

**[!UICONTROL この質問を今後確認しない]** を選択した場合は、このプロンプトをリセットできます。 Windows レジストリの編集に慣れたシステム管理者のみが、次の変更を行う必要があります。

1. **[!UICONTROL スタート/]** を実行メニューの **regedit** コマンドを使用して、レジストリエディタを開きます。

1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade** エントリを削除し、レジストリエディタを閉じます。

>[!NOTE]
>
>既存の実装に更新されたコンソールを適用する場合、クライアントコンソールを更新するよう求めるプロンプトがユーザーに自動的に表示されます。 初めて Campaign を実装する場合、ユーザーはコンソールをダウンロードする必要があります。 両方のオプションの詳細については、以下を参照してください

### 既存の実装用にコンソールを更新する{#update-the-client-console}

コンソールが Campaign サーバーフォルダーで使用可能になると、最新のクライアントコンソールバージョンをポップアップウィンドウでダウンロードするように求められます。

**更新を完了するには、管理者アクセス権が必要です。ユーザーが管理者権限を持っていない場合、システム管理者はすべてのクライアントコンソールにデプロイする必要があります**


### 新しい実装用にコンソールをダウンロードします。{#download-the-client-console}

ユーザーは、次の手順に従ってコンソールをダウンロードし、インストールする必要があります。

1. Web ブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   [`https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp`](https://myserver.adobe.com/nl/jsp/logon.jsp).

1. 識別ウィンドウで、ログイン名とパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成時に定義した内部アカウントの資格情報を使用します。

1. インストールページの **[!UICONTROL ダウンロード]** リンクをクリックします。
1. クライアントセットアップファイルをダウンロードして保存します。
1. Windows のコンピューターでダウンロードしたファイルを実行します。インストールが開始します。 クライアントコンソールのデフォルトのインストールパスは **$PROGRAMFILES$/Adobe/Adobe Campaign Classic vX クライアント** です。「X」はAdobe Campaignのバージョンに応じて「6」または「7」です。

### 接続の作成（初回ユーザーのみ）{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. **Adobe Campaign** プログラムグループの Windows の **[!UICONTROL 開始]** メニューからコンソールを起動します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプの URL を使用できます。

1. Adobe IMSが組織に対して設定されている場合は、「**[!UICONTROL Adobe IDに接続]**」オプションをオンにします。

1. 「**[!UICONTROL OK]**」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼動環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

### Adobe Campaign へのログオン

既存のインスタンスにログオンするには、以下の手順に従います。

1. **Adobe Campaign** プログラムグループの Windows の **[!UICONTROL 開始]** メニューからコンソールを起動します。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要がある Campaign インスタンスを選択します。

1. 「**[!UICONTROL OK]**」をクリックします。

1. ユーザーのログイン資格情報を入力し、「**[!UICONTROL ログイン]**」をクリックします。


**関連トピック**

* [インスタンスの作成とログイン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)

## チュートリアルビデオ

このビデオでは、Adobe Campaign Client のインストールおよび設定方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/35124?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
