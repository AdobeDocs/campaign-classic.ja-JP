---
solution: Campaign Classic
product: campaign
title: Windows 用クライアントコンソールの可用性
description: Windows 用クライアントコンソールの可用性
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
translation-type: tm+mt
source-git-commit: 1b02c3870ddc01705f01ea992e734cf0810e003a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---


# Windows 用クライアントコンソールの可用性{#client-console-availability-for-windows}

作成および設定したインスタンスにログオンできるAdobe Campaignユーザーには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

Adobe Campaignアプリケーションサーバー(**nlserver web**)の開始に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取る場合、HTMLインターフェイスを介してAdobe Campaignリッチクライアントのセットアッププログラムを使用できるように設定できます。 クライアントコンソールの新しいバージョンが利用可能になった場合は、ユーザーはクライアントコンソールを起動する際に、ダウンロードするよう招待されます。

これを行うには、次の操作を行う必要があります。

1. コンソールのインストールプログラムを含むパッケージを選択します。

   このファイルはv7では`setup-client-7.X.XXXX.exe`、v6.1では`setup-client-6.X.XXXX.exe`と呼ばれます。`X`はAdobe Campaignのサブバージョン、`XXXX`はビルド番号です。

1. このパッケージを、（ハイブリッドインストールの場合はマーケティングサーバーの）Adobe Campaignーのインストールフォルダー&#x200B;**/datakit/nl/eng/jsp**&#x200B;の下のフォルダーにコピー&amp;ペーストします。
1. 開始Adobe Campaignサーバー。

キャンペーンユーザーは、次のURLを使用して、Webブラウザーを介してコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されているログインとパスワードが必要です。

このセクション](../../installation/using/installing-the-client-console.md)で、コンソール[のインストール方法を説明します。

## エンドユーザーにクライアントコンソールのアップグレードを提案する

コンソールがキャンペーンサーバーフォルダーで使用可能になると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするよう招待されます。 Adobeでは、**[!UICONTROL 「この質問]**&#x200B;は選択しないでください」オプションを選択し、コンソールの新しいバージョンが利用可能な場合にすべてのユーザーに警告が表示されるようにすることをお勧めします。

このオプションを選択して、最新バージョンをダウンロードしないことを選択した場合、他のユーザーには新しいバージョンが通知されません。

このオプションが選択されている場合は、このプロンプトをリセットできます。 次の変更を行うのは、Windowsレジストリの編集に慣れたシステム管理者のみです。

1. **[!UICONTROL 開始/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリエディターを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade**&#x200B;エントリを削除し、レジストリエディターを閉じます。

