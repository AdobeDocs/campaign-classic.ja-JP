---
title: Windows 用クライアントコンソールの可用性
seo-title: Windows 用クライアントコンソールの可用性
description: Windows 用クライアントコンソールの可用性
seo-description: null
page-status-flag: never-activated
uuid: d1cbb34e-87e0-481b-a78b-3616047eb5cb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: 4fa2e8c1-33d1-4d14-941b-ca528b8ceabb
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 6%

---


# Windows 用クライアントコンソールの可用性{#client-console-availability-for-windows}

作成および設定したインスタンスにログオンできるAdobe Campaignユーザーには、クライアントコンソールを使用する必要があります。

Adobe Campaignアプリケーションサーバー(**nlserver web**)の開始に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取る場合、HTMLインターフェイスを介してAdobe Campaignリッチクライアントのセットアッププログラムを使用できるように設定できます。

これを行うには、次の操作を行う必要があります。

1. コンソールのインストールプログラムを含むパッケージを回復します。

   このファイルはv7またはv6.1 `setup-client-7.X.XXXX.exe` で呼び出されます。ここで、 `setup-client-6.X.XXXX.exe` はAdobe Campaignのサブバージョンで、 `X``XXXX` はビルド番号です。

1. このパッケージをコピーして、/datakit/nl/eng/jspの下のAdobe Campaignーのインストールフォルダー **に貼り付けます**。
1. Adobe Campaignサーバーの開始。

最終ユーザは、次のURLにより、ウェブブラウザを介してコンソールインストールプログラムをダウンロードすることができます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されているログインとパスワードが必要です。

コンソールをダウンロードしてインストールするには、「クライアントコンソールの [インストール](../../installation/using/installing-the-client-console.md)」を参照してください。

新しいバージョンのクライアントコンソールが利用可能になった場合は、必ずそのコンソールのダウンロードを招待されます。

>[!NOTE]
>
>表示されるプロンプトで、「この質問を表示しない」オプションを **** 選択しないままにして、コンソールの新しいバージョンが利用可能な場合にすべてのAdobeに警告が表示されるようにすることをお勧めします。\
>このオプションを選択して、最新バージョンをダウンロードしないことを選択した場合、他のユーザーには新しいバージョンが通知されません。

このプロンプトをリセットするには、次の手順に従います（レジストリの編集に慣れたシステム管理者のみがこれらの変更を行う必要があります）。

1. レジストリ/実行 **(Run** )メニューから、regedit **** (regedit)コマンドを使用してレジストリエディタを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. confAdvisedUpgradeエントリを削除し **、レジストリエディターを閉じます** 。

