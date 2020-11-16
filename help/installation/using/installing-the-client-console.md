---
title: クライアントコンソールのインストール
description: クライアントコンソールのインストール方法
page-status-flag: never-activated
uuid: 1279c0d8-bf27-4a58-ae94-796d6147231a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: d1069b23-e08d-43c5-bbfb-3158ac40dc7e
translation-type: tm+mt
source-git-commit: 6d6f63fb6ac99c3a9e58a8670bc9bc59e6cfd420
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 13%

---


# キャンペーンクライアントコンソールのインストール{#installing-the-client-console}

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。

起動する前に、キャンペーン [互換性マトリックスを確認し、キャンペーンサーバーのURLとユーザーの資格情報を取得する必要があります](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)。

>[!CAUTION]
>
>キャンペーンクライアントコンソールとキャンペーンアプリケーションサーバーは、同じ製品バージョンで実行する必要があります。 Adobeでは、同じ製品ビルドを使用することもお勧めします。

## コンソールをダウンロード{#download-the-client-console}

Adobe Campaignクライアントコンソールをダウンロードしてインストールするには、次の手順に従います。

1. Webブラウザーを開き、次のアドレスからコンソールをダウンロードします。

   [`https://<your adobe campaign server>:<port number>/nl/jsp/logon.jsp`](https://myserver.adobe.com/nl/jsp/logon.jsp).

1. IDウィンドウで、ログイン名とパスワードを入力します。

   ![](assets/s_ncs_install_setup_download01.png)

   必要に応じて、インスタンスの作成時に定義した内部アカウントの資格情報を使用します。

1. インストールページの **[!UICONTROL ダウンロード]** リンクをクリックします。
1. クライアントセットアップファイルをダウンロードして保存します。
1. Windowsのコンピューターで、ダウンロードしたファイルを実行します。インストール開始がアップになります。 クライアントコンソールのデフォルトのインストールパスは、 **$PROGRAMFILES$/Adobe/Adobe Campaign ClassicvX Client**&#x200B;です。「X」は、Adobe Campaignのバージョンに応じて「6」または「7」になります。

>[!NOTE]
>
>Windowsでは、 **nlclient.exe** ファイルをWindowsサーバー上の `[INSTALL]/bin` ディレクトリから直接起動できます。ここで、はAdobe Campaignのインストールフォルダーのアクセスパス `[INSTALL]` です。

## 接続の作成{#create-the-connection}

クライアントコンソールをインストールしたら、次の手順に従ってアプリケーションサーバーへの接続を作成します。

1. [Windows **[!UICONTROL 開始]** ]メニューの[ **Adobe Campaign** プログラム]でコンソールを開始します。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **** 追加/Connectionをクリックし、Adobe CampaignアプリケーションサーバーのラベルとURLを入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URLを介したAdobe Campaignアプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、またはIPアドレスを使用します。

   例えば、 [`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプURLを使用できます。

1. AdobeIMSが組織に対して設定されている場合は、「 **[!UICONTROL Adobe IDに接続」オプションをオンにします]**

1. 「 **[!UICONTROL OK]** 」をクリックして設定を保存します。

例えば、テスト、ステージ、実稼働環境に接続するために必要な数の接続を追加できます。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

## Adobe Campaignへのログオン

既存のインスタンスにログオンするには、次の手順に従います。

1. [Windows **[!UICONTROL 開始]** ]メニューの[ **Adobe Campaign** プログラム]でコンソールを開始します。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。

1. ログインする必要があるキャンペーンインスタンスを選択します。

1. Click **[!UICONTROL Ok]**

1. ユーザーログイン資格情報を入力し、「 **[!UICONTROL ログイン」をクリックします]**

**関連トピック**

* [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).
* [互換性マトリックス](https://helpx.adobe.com/jp/campaign/kb/compatibility-matrix.html)
* [Adobe Campaignクライアントのインストールとセットアップ](https://docs.adobe.com/content/help/en/campaign-classic-learn/tutorials/getting-started/install-and-setup-the-adobe-campaign-client.html) （ビデオ）
