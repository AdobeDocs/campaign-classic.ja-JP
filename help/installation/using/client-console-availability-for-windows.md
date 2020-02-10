---
title: Windows向けクライアントコンソールの可用性
seo-title: Windows向けクライアントコンソールの可用性
description: Windows向けクライアントコンソールの可用性
seo-description: null
page-status-flag: never-activated
uuid: d1cbb34e-87e0-481b-a78b-3616047eb5cb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: 4fa2e8c1-33d1-4d14-941b-ca528b8ceabb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# Windows向けクライアントコンソールの可用性{#client-console-availability-for-windows}

Adobe Campaignユーザーが作成し設定したインスタンスにログオンできるようにするには、クライアントコンソールを使用する必要があります。

Adobe Campaignアプリケーションサーバー(**nlserver web**)の起動に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取った場合、Adobe CampaignリッチクライアントのセットアッププログラムをHTMLインターフェイス経由で使用できるように設定できます。

これを行うには、次の操作を行う必要があります。

1. コンソールインストールプログラムを含むパッケージを回復します。

   このファイルはv7 `setup-client-7.X.XXXX.exe` または `setup-client-6.X.XXXX.exe` for v6.1で呼び出されます。 `X` はAdobe Campaignのサブバージョンで、はビルド `XXXX` 番号です。

1. このパッケージを/datakit/nl/eng/jspの下のAdobe Campaignインストー **ルフォルダーにコピーして貼り付けます**。
1. Adobe Campaignサーバーを起動します。

最終的なユーザは、次のURLに感謝して、ウェブブラウザを通じてコンソールインストールプログラムをダウンロードすることができる。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されたログインとパスワードが必要です。

コンソールをダウンロードしてインストールするには、「クライアントコンソ [ールのインストール」を参照してくださ](../../installation/using/installing-the-client-console.md)い。

新しいバージョンのクライアントコンソールが利用可能になった場合は、必ずダウンロードを招待されます。

>[!NOTE]
>
>表示されるプロンプトで、コンソールの新しいバージョンが利用可能な場合にすべてのユーザーに警告が表示されるように、このオプシ **[!UICONTROL No longer ask this question]** ョンを選択しないでおくことをお勧めします。\
>このオプションを選択し、最新バージョンをダウンロードしないように選択した場合、利用可能な新しいバージョンは他のユーザーに通知されません。

このプロンプトをリセットするには、次の手順に従います（レジストリの編集に慣れているシステム管理者のみが変更を加えます）。

1. メニューからregeditコマンドを使用し **て、レジストリ** ・エディタを **[!UICONTROL Start > Run]** 開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. confAdvisedUpgradeエントリを削 **除し** 、レジストリエディターを閉じます。

