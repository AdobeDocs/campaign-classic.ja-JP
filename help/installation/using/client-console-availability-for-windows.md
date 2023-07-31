---
product: campaign
title: Windows でのクライアントコンソールの可用性
description: Windows でのクライアントコンソールの可用性
feature: Installation, Upgrade
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 57845eae-1f1a-42f4-b2ba-46d454677ae0
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 10%

---

# Windows でのクライアントコンソールの可用性{#client-console-availability-for-windows}



Adobe Campaignユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

コンピューターがAdobe Campaignアプリケーションサーバー (**nlserver web**) はクライアントコンソールからユーザー接続を受け取るので、Adobe Campaignリッチクライアントの設定プログラムをHTMLインターフェイスから使用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能な場合は、クライアントコンソールを起動する際に、ユーザーに招待してダウンロードしてもらいます。

そのためには、次の手順を実行する必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルの名前はです。 `setup-client-7.X.XXXX.exe`です。 `X` はAdobe Campaignのサブバージョンで、 `XXXX` は、ビルド番号です。

1. このパッケージを、次の場所にある（ハイブリッドインストールの場合はマーケティングサーバーの）Adobe Campaignインストールフォルダーにコピー&amp;ペーストします。 **/datakit/nl/eng/jsp**.
1. Adobe Campaignサーバーを起動します。

Campaign ユーザーは、次の URL を使用して、Web ブラウザーからコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソールのインストール方法を説明します。 [この節](../../installation/using/installing-the-client-console.md).

## エンドユーザーにクライアントコンソールをアップグレードするよう提案する

コンソールが Campaign サーバーフォルダーで使用可能になると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするように招待されます。 Adobeは、オプションを終了することをお勧めします **[!UICONTROL 今後この質問をしない]** コンソールの新しいバージョンが利用可能になったときにすべてのユーザーに警告が表示されるようにするには、選択を解除します。

このオプションを選択し、最新バージョンをダウンロードしない場合、他のユーザーには、新しい利用可能なバージョンについて通知されません。

このオプションが選択されている場合は、このプロンプトをリセットできます。 以下の変更を行うのは、Windows レジストリの編集に慣れたシステム管理者のみです。

1. 次を使用してレジストリエディターを開く： **regedit** 命令 **[!UICONTROL スタート/実行]** メニュー。
1. ノードを検索し、展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. を削除します。 **confAdvisedUpgrade** レジストリエディタを開き、閉じます。
