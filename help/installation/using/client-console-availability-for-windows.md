---
product: campaign
title: Windows でのクライアントコンソールの可用性
description: Windows でのクライアントコンソールの可用性
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 57845eae-1f1a-42f4-b2ba-46d454677ae0
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Windows でのクライアントコンソールの可用性{#client-console-availability-for-windows}

![](../../assets/v7-only.svg)

Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

Adobe Campaignアプリケーションサーバー (**nlserver web**) の起動に使用されたコンピューターがクライアントコンソールからユーザー接続を受け取った場合、HTMLインターフェイスを介してAdobe Campaignのリッチクライアントのセットアッププログラムを使用できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動すると、そのコンソールをダウンロードするように招待されます。

これをおこなうには、次の操作をおこなう必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは、v7 の場合は `setup-client-7.X.XXXX.exe`、v6.1 の場合は `setup-client-6.X.XXXX.exe` と呼ばれ、`X` はAdobe Campaignのサブバージョン、`XXXX` はビルド番号です。

1. このパッケージを、（ハイブリッドインストールのマーケティングサーバーの）Adobe Campaignインストールフォルダーの **/datakit/nl/eng/jsp** の下にコピーして貼り付けます。
1. Adobe Campaignサーバーを起動します。

次の URL を使用すると、Campaign ユーザーは、Web ブラウザーを使用してコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソール [ のインストール方法については、この節 ](../../installation/using/installing-the-client-console.md) を参照してください。

## エンドユーザーにクライアントコンソールのアップグレードを提案する

コンソールが Campaign サーバーフォルダーで使用可能になると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするように招待されます。 Adobeは、「**[!UICONTROL この質問]** は選択しないでください」オプションを選択したままにして、新しいバージョンのコンソールが利用可能になったときにすべてのユーザーに警告が表示されるようにすることをお勧めします。

このオプションを選択し、最新バージョンをダウンロードしないことを選択した場合、他のユーザーには新しい利用可能なバージョンが通知されません。

このオプションを選択した場合は、このプロンプトをリセットできます。 Windows レジストリの編集に慣れたシステム管理者のみが、次の変更を行う必要があります。

1. **[!UICONTROL スタート/]** を実行メニューの **regedit** コマンドを使用して、レジストリエディタを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade** エントリを削除し、レジストリエディタを閉じます。
