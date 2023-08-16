---
product: campaign
title: インスタンスの作成とログイン
description: インスタンスの作成とログイン
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 18%

---

# インスタンスの作成とログイン{#creating-an-instance-and-logging-on}



新しいインスタンスと Adobe Campaign データベースを作成するには、次の手順を実行します。

1. 接続の作成.
1. ログオンして、関連するインスタンスを作成します。
1. データベースの作成と設定.

>[!NOTE]
>
>これらの操作を実行できるの **は内部** 識別子だけです。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaign コンソールを起動すると、ログインページにアクセスできるようになります。

新しいインスタンスを作成するには、以下の手順をフォローするます。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。このリンクは、 **[!UICONTROL 新規…]** または既存のインスタンス名

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、`https://<machine>.<domain>.com` タイプの URL を使用できます。

   >[!CAUTION]
   >
   >接続 URL の場合、、、およびダッシュ (-) またはフルストップのみを使用 `[a-z]` `[A-Z]` `[0-9]` します。

1. 「Ok」 ]**をクリックし**[!UICONTROL  て設定を確認します。これで、インスタンス作成プロセスを開始できます。
1. **[!UICONTROL 接続設定]** ウィンドウで、内部 **ログインとそのパスワードを入力** して、Adobe Campaign アプリケーションサーバーに接続します。接続すると、インスタンス作成ウィザードにアクセスして新しいインスタンスを宣言します。
1. **[!UICONTROL 「名前]** 」フィールドにインスタンス名 **を入力** します。この名前は設定ファイル **`<instance>` の .xml** を生成するために使用され、コマンドラインパラメーターでインスタンスを識別するために使用されます。特殊文字を含まない短い名前を選択していることを確認してください。 例: **eMarketing**

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は 40 文字以内にする必要があります。 これにより、「メッセージ」ヘッダーのサイズを制限し、特に SpamAssassin などのツールによってメッセージがスパムと見なされないようにすることができます。

1. Adobe Analytics の **[!UICONTROL DNS マスク]** フィールドに、 **DNS マスクのリスト** インスタンスを添付する先のインスタンス。 Adobe Campaignサーバーは、HTTP リクエストに表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は文字列の間に含まれます **https://** 最初のスラッシュ文字 **/** の名前を指定します。

   コンマで区切られた値のリストを定義できます。

   null ? &#42;文字をワイルドカードとして使用して、1つまたは複数の文字 (DNS、ポートなど) を置き換えることができます。インスタンスについては、 **「https://demo:8080」と均等「https://demo2」のように、デモ&#42;** の値は「https://demo」で動作します。

   使用する名前は、DNS で定義されている必要があります。 また、Windows および **Linux の/etc/hosts** ファイル内で、DNS 名と IP アドレスの通信を c:/windows/system32/drivers/etc/hosts **ファイルに** 通知することもできます。したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   サーバーは、特に e メールで画像をアップロードする場合、この名前で識別する必要があります。

   さらに、サーバーは、この名前によって自身に接続でき、可能であれば、(特に PDF 形式でのレポートのエクスポートを許可するために) ループバックアドレス-127.0.0.1-を使用する必要があります。

1. Adobe Analytics の **[!UICONTROL 言語]** ドロップダウンリストから、 **インスタンス言語**：英語（米国）、英語（英国）、フランス語、日本語。

   英語（米国）と英語（英国）の違いについては、 [この節](../../platform/using/adobe-campaign-workspace.md#date-and-time).

   >[!CAUTION]
   >
   >この手順の後は、インスタンスの言語を変更できません。 Adobe Campaignインスタンスは多言語ではありません。インターフェイスを言語から別の言語に切り替えることはできません。

1. 「Ok」 ]**をクリックし**[!UICONTROL  てインスタンス宣言を確認します。ログオフしてから再度ログインしてデータベースを宣言します。

   >[!NOTE]
   >
   >インスタンスはコマンドラインから作成できます。 詳しくは、コマンドライン ](../../installation/using/command-lines.md) を [ 参照してください。
