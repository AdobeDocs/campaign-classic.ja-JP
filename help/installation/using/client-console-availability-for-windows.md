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
source-wordcount: '346'
ht-degree: 8%

---

# Windows でのクライアントコンソールの可用性{#client-console-availability-for-windows}



Adobe Campaign ユーザーが、作成および設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

## クライアントコンソールを使用可能にする

Adobe Campaign アプリケーションサーバーの起動に使用するコンピューター（**nlserver web**）がクライアントコンソールからユーザー接続を受け取ると、それを設定して、Adobe Campaign リッチクライアントの設定プログラムをHTMLインターフェイスで使用できるようになります。 クライアントコンソールの新しいバージョンが利用可能になると、クライアントコンソールの起動時にユーザーがクライアントコンソールをダウンロードするように招待されます。

そのためには、次の手順を実行する必要があります。

1. コンソールインストールプログラムを含むパッケージを選択します。

   このファイルは `setup-client-7.X.XXXX.exe` という名前です（`X` はAdobe Campaignのサブバージョン、`XXXX` はビルド番号）。

1. このパッケージをコピーして、（ハイブリッドインストールの場合はマーケティングサーバー上の）Adobe Campaign インストールフォルダーの **/datakit/nl/eng/jsp** の下に貼り付けます。
1. Adobe Campaign サーバーを起動します。

Campaign ユーザーは、次の URL により、web ブラウザーからコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソールのインストール方法について詳しくは [&#x200B; この節 &#x200B;](../../installation/using/installing-the-client-console.md) を参照してください。

## クライアントコンソールのアップグレードについてエンドユーザーに提案する

Campaign サーバーフォルダーでコンソールを使用できるようになると、ユーザーは、専用のプロンプトウィンドウで最新のクライアントコンソールバージョンをダウンロードするように招待されます。 Adobeは、コンソールの新しいバージョンが利用可能になったときにすべてのユーザーにアラートが送信されるようにするために、「**[!UICONTROL 今後この質問をしない]**」オプションを選択しないままにすることをお勧めします。

このオプションを選択して最新バージョンをダウンロードしないことを選択した場合、利用可能な新しいバージョンは他のユーザーには通知されません。

オプションを選択した場合は、このプロンプトをリセットできます。 Windows レジストリの編集に慣れているシステム管理者だけが、次の変更を行う必要があります。

1. **スタート/ファイル名を指定して実行** メニューから **[!UICONTROL regedit]** コマンドを使用してレジストリエディターを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade** エントリを削除し、レジストリエディターを閉じます。
