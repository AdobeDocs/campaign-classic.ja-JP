---
title: インスタンスの作成とログオン
seo-title: インスタンスの作成とログオン
description: インスタンスの作成とログオン
seo-description: null
page-status-flag: never-activated
uuid: cb1620b3-f6e8-41dc-9142-ac0da65b6f8d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: c7395094-c635-45ab-8455-a050f7d16b64
translation-type: tm+mt
source-git-commit: 6d6f63fb6ac99c3a9e58a8670bc9bc59e6cfd420
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 4%

---


# インスタンスの作成とログオン{#creating-an-instance-and-logging-on}

新しいインスタンスとAdobe Campaign・データベースを作成するには、次のプロセスを適用します。

1. 接続を作成します。
1. ログオンして、関連するインスタンスを作成します。
1. データベースを作成し、設定します。

>[!NOTE]
>
>これらの操作を実行できるのは **内部** IDのみです。 For more on this, refer to [Internal identifier](../../installation/using/campaign-server-configuration.md#internal-identifier).

Adobe Campaignコンソールを起動すると、ログインページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。 このリンクは、 **** 新規…または既存のインスタンス名にすることができます。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **** 追加/Connectionをクリックし、Adobe CampaignアプリケーションサーバーのラベルとURLを入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URLを介したAdobe Campaignアプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、またはIPアドレスを使用します。

   例えば、 [`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプURLを使用できます。

   >[!CAUTION]
   >
   >接続URLには、次の文字のみを使用します。 `[a-z]`、 `[A-Z]`、 `[0-9]` ダッシュ(-)またはフルストップ

1. 「 **[!UICONTROL OK]** 」をクリックして設定を確認します。これで、インスタンス作成プロセスから開始できます。
1. 「 **[!UICONTROL Connection settings]** 」ウィンドウで、 **** 内部ログインと、Adobe Campaignアプリケーションサーバーに接続するためのパスワードを入力します。 接続が完了したら、インスタンス作成ウィザードにアクセスして新しいインスタンスを宣言します
1. 「 **[!UICONTROL 名前]** 」フィールドに、 **インスタンス名を入力します**。 設定ファイルの **config-`<instance>`.xmlの生成に使用され、コマンドラインパラメーターでインスタンスの識別に使用されるので** 、特殊文字を含まない短い名前を選択する必要があります。 次に例を示します。 **eMarketing**。

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は40文字以下にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、特にSpamAssicinなどのツールでメッセージがスパムと見なされるのを防ぐことができます。

1. [ **[!UICONTROL DNSマスク]** ]フィールドに、インスタンスをアタッチするDNSマスク **** リストを入力します。 Adobe Campaignサーバーは、HTTPリクエストに表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は、文字列https:// **と、サーバーアドレスの先頭のスラッシュ** / **** との間に含まれます。

   値のリストをカンマで区切って定義できます。

    ? また、1つまたは複数の文字（DNS、ポートなど）を置き換える場合は、ワイルドカードとして*文字を使用できます。 例えば、 **demo*** 値は「https://demo」と共に使用でき、「https://demo:8080」と「https://demo2」と同様に使用できます。

   使用する名前は、DNSで定義する必要があります。 また、Windowsの **c:/windows/system32/drivers/etc/hosts** ファイルとLinuxの/etc/hosts **** ファイルにあるDNS名とIPアドレスの通信を通知することもできます。 したがって、選択したインスタンスに接続するには、このDNS名を使用するように接続設定を変更する必要があります。

   サーバーは、特に電子メールで画像をアップロードする場合、この名前で識別する必要があります。

   さらに、サーバはこの名前で自身に接続でき、可能であればループバックアドレス127.0.0.1で接続できる必要があります。特に、レポートをPDF形式でエクスポートできるようにするためです。

1. 「 **[!UICONTROL 言語]** 」ドロップダウンリストで、 **インスタンスの言語を選択します**。英語（米国）、英語（英国）、フランス語または日本語。

   本項では、米国英語と英国英語の違いにつ [いて説明](../../platform/using/adobe-campaign-workspace.md#date-and-time)。

   >[!CAUTION]
   >
   >この手順の後でインスタンス言語を変更することはできません。 Adobe Campaignインスタンスが多言語ではありません：インターフェイスを言語から別の言語に切り替えることはできません。

1. 「 **[!UICONTROL OK]** 」をクリックしてインスタンスの宣言を確定します。 ログオフしてから再度ログオンし、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスは、コマンドラインから作成できます。 For more on this, refer to [Command lines](../../installation/using/command-lines.md).

