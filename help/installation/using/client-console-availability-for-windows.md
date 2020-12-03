---
solution: Campaign Classic
product: campaign
title: Windows 用クライアントコンソールの可用性
description: Windows 用クライアントコンソールの可用性
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
translation-type: tm+mt
source-git-commit: c625b4109e2cb47446331cd009ff9827c8267c93
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 5%

---


# Windows 用クライアントコンソールの可用性{#client-console-availability-for-windows}

作成および設定したインスタンスにログオンできるAdobe Campaignユーザーには、クライアントコンソールを使用する必要があります。

Adobe Campaignアプリケーションサーバー(**nlserver web**)の開始に使用されるコンピューターがクライアントコンソールからユーザー接続を受け取る場合、HTMLインターフェイスを介してAdobe Campaignリッチクライアントのセットアッププログラムを使用できるように設定できます。

これを行うには、次の操作を行う必要があります。

1. コンソールのインストールプログラムを含むパッケージを回復します。

   このファイルはv7では`setup-client-7.X.XXXX.exe`、v6.1では`setup-client-6.X.XXXX.exe`と呼ばれます。`X`はAdobe Campaignのサブバージョン、`XXXX`はビルド番号です。

1. このパッケージを&#x200B;**/datakit/nl/eng/jsp**&#x200B;の下のAdobe Campaignインストールフォルダーにコピー&amp;ペーストします。
1. Adobe Campaignサーバーの開始。

最終ユーザーは、次のURLの指示に従って、Webブラウザーを介してコンソールインストールプログラムをダウンロードできます。

```
https://<your Adobe Campaign server>:>port number>/nl/jsp/logon.jsp
```

このページには、アプリケーションで定義されているログインとパスワードが必要です。

コンソールをダウンロードしてインストールするには、「[クライアントコンソールのインストール](../../installation/using/installing-the-client-console.md)」を参照してください。

新しいバージョンのクライアントコンソールが利用可能になった場合は、必ずそのコンソールのダウンロードを招待されます。

>[!NOTE]
>
>表示されるプロンプトで、「**[!UICONTROL この質問]**&#x200B;は選択しないでください。」を選択すると、コンソールの新しいバージョンが利用可能になったときにすべてのユーザーに警告が表示されます。\
>このオプションを選択して、最新バージョンをダウンロードしないことを選択した場合、他のユーザーには新しいバージョンが通知されません。

このプロンプトをリセットするには、次の手順に従います（レジストリの編集に慣れたシステム管理者のみがこれらの変更を行う必要があります）。

1. **[!UICONTROL 開始/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリエディターを開きます。
1. ノードを検索して展開します。

   ```
   \HKEY_CURRENT_USER\Software\Neolane\NL_6\nlclient
   ```

1. **confAdvisedUpgrade**&#x200B;エントリを削除し、レジストリエディターを閉じます。

