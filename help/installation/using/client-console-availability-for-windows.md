---
product: campaign
title: Windows でのクライアントコンソールの可用性
description: Windows でのクライアントコンソールの可用性
feature: Installation, Upgrade
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 57845eae-1f1a-42f4-b2ba-46d454677ae0
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 13%

---

# Windows でのクライアントコンソールの可用性{#client-console-availability-for-windows}



Adobe Campaign ユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

Adobe Campaign アプリケーションサーバー（**nlserver web**）を起動するために使用されるコンピューターがクライアントコンソールからユーザー接続を受け取った場合、HTML インターフェイスを介してAdobe Campaign リッチクライアントのセットアッププログラムを利用できるように設定できます。 新しいバージョンのクライアントコンソールが使用可能になると、クライアントコンソールの起動時にダウンロードするようにユーザーが招待されます。

そのためには、次の手順を実行する必要があります。

1. コンソールのインストールプログラムを含むパッケージを選択します。

   このファイルは`setup-client-7.X.XXXX.exe`と呼ばれます。ここでは、`X`はAdobe Campaignのサブバージョンで、`XXXX`はビルド番号です。

1. このパッケージをコピーして、**/datakit/nl/eng/jsp**&#x200B;の下のAdobe Campaign インストールフォルダー（ハイブリッドインストール用のマーケティングサーバー上）に貼り付けます。
1. Adobe Campaign serverを起動します。

Campaign ユーザーは、次のURLを使用して、web ブラウザー経由でコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソール [のインストール方法については、この節](../../installation/using/installing-the-client-console.md)を参照してください。

## エンドユーザーにクライアントコンソールのアップグレードを提案する

コンソールがCampaign サーバーフォルダーで使用可能になると、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするようにユーザーが招待されます。 Adobeでは、新しいバージョンのコンソールが使用可能になったときに、すべてのユーザーにアラートが通知されるようにするために、「**[!UICONTROL この質問に対する回答]**&#x200B;を選択解除しなくなります」オプションをオフにすることをお勧めします。

このオプションを選択し、最新バージョンをダウンロードしないことを選択した場合、他のユーザーに使用可能な新しいバージョンが通知されることはありません。

オプションを選択した場合は、このプロンプトをリセットできます。 Windows レジストリの編集に慣れているシステム管理者のみが、次の変更を行う必要があります。

1. **[!UICONTROL 開始/実行]** メニューから&#x200B;**regedit** コマンドを使用してレジストリエディターを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade** エントリを削除し、レジストリエディターを閉じます。
