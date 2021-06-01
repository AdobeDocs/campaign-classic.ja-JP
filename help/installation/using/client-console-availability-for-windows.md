---
product: campaign
title: Windows でのクライアントコンソールの可用性
description: Windows でのクライアントコンソールの可用性
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 57845eae-1f1a-42f4-b2ba-46d454677ae0
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Windows でのクライアントコンソールの可用性{#client-console-availability-for-windows}

Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

Adobe Campaignアプリケーションサーバー(**nlserver web**)の起動に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取ったら、Adobe CampaignリッチクライアントのセットアッププログラムをHTMLインターフェイスで使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動すると、そのコンソールをダウンロードするようにユーザーが招待されます。

これをおこなうには、次の操作を行う必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、v7の場合は`setup-client-7.X.XXXX.exe`、v6.1の場合は`setup-client-6.X.XXXX.exe`と呼ばれ、`X`はAdobe Campaignのサブバージョン、`XXXX`はビルド番号です。

1. このパッケージを、（ハイブリッドインストールのマーケティングサーバーの）Adobe Campaignインストールフォルダーの&#x200B;**/datakit/nl/eng/jsp**&#x200B;の下にコピーして貼り付けます。
1. Adobe Campaignサーバーを起動します。

次のURLを使用すると、Campaignユーザーは、Webブラウザーを使用してコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

この節](../../installation/using/installing-the-client-console.md)で、コンソール[のインストール方法を説明します。

## エンドユーザーにクライアントコンソールのアップグレードを提案する

コンソールがCampaignサーバーフォルダーで使用可能になると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするよう招待されます。 Adobeは、「**[!UICONTROL この質問]**&#x200B;は選択しないでください」オプションを選択し、新しいバージョンのコンソールが利用可能になったときにすべてのユーザーに警告が表示されるようにすることをお勧めします。

このオプションを選択し、最新バージョンをダウンロードしないことを選択した場合、他のユーザーには新しい利用可能なバージョンが通知されません。

このオプションを選択した場合は、このプロンプトをリセットできます。 以下の変更は、Windowsレジストリの編集に慣れたシステム管理者のみが行う必要があります。

1. **[!UICONTROL スタート/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリエディターを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade**&#x200B;エントリを削除し、レジストリエディターを閉じます。
