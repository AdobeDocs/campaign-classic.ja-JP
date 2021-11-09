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

コンピューターがAdobe Campaignアプリケーションサーバー (**nlserver web**) はクライアントコンソールからユーザー接続を受け取るので、Adobe Campaignリッチクライアントの設定プログラムをHTMLインターフェイスから使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動する際に、ユーザーに招待してダウンロードしてもらいます。

これをおこなうには、次の操作が必要です。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルの名前はです。 `setup-client-7.X.XXXX.exe` v7 または `setup-client-6.X.XXXX.exe` v6.1 の場合は、 `X` はAdobe Campaignのサブバージョンで、 `XXXX` はビルド番号です。

1. このパッケージを、次の場所にある（ハイブリッドインストールの場合はマーケティングサーバーの）Adobe Campaignインストールフォルダーにコピー&amp;ペーストします。 **/datakit/nl/eng/jsp**.
1. Adobe Campaignサーバーを起動します。

Campaign ユーザーは、次の URL を使用して、Web ブラウザーからコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソールのインストール方法を説明します [この節](../../installation/using/installing-the-client-console.md).

## エンドユーザーにクライアントコンソールをアップグレードするよう提案する

コンソールが Campaign サーバーフォルダーで使用可能になると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするように招待されます。 Adobeは、オプションを終了することをお勧めします **[!UICONTROL 今後この質問をしない]** コンソールの新しいバージョンが利用可能になったときにすべてのユーザーに警告が表示されるようにするには、選択を解除します。

このオプションを選択し、最新バージョンをダウンロードしない場合、他のユーザーには、新しい利用可能なバージョンについて通知されません。

このオプションが選択されている場合は、このプロンプトをリセットできます。 以下の変更を行うのは、Windows レジストリの編集に慣れたシステム管理者のみです。

1. 次を使用してレジストリエディターを開く： **regedit** 命令 **[!UICONTROL スタート/実行]** メニュー
1. ノードを検索し、展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. を削除します。 **confAdvisedUpgrade** レジストリエディタを開き、閉じます。
