---
product: campaign
title: インスタンスの作成とログイン
description: インスタンスの作成とログイン
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 16%

---

# インスタンスの作成とログイン{#creating-an-instance-and-logging-on}

![](../../assets/v7-only.svg)

新しいインスタンスとAdobe Campaignデータベースを作成するには、次の手順に従います。

1. 接続を作成します。
1. ログオンして、関連するインスタンスを作成します。
1. データベースの作成と設定.

>[!NOTE]
>
>これらの操作を実行できるのは、**内部** 識別子だけです。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaignコンソールを起動したら、ログインページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。このリンクは **[!UICONTROL 新規…]** または既存のインスタンス名。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com) タイプの URL を使用できます。

   >[!CAUTION]
   >
   >接続 URL には、次の文字のみを使用します。`[a-z]`、`[A-Z]`、`[0-9]`、ダッシュ (-) またはフルストップ。

1. 「**[!UICONTROL OK]**」をクリックして設定を確認します。これで、インスタンス作成プロセスから始めることができます。
1. **[!UICONTROL 接続設定]** ウィンドウで、**内部** ログインと、Adobe Campaignアプリケーションサーバーに接続するためのパスワードを入力します。 接続したら、インスタンス作成ウィザードにアクセスして、新しいインスタンスを宣言します
1. 「**[!UICONTROL 名前]**」フィールドに、**インスタンス名** を入力します。 この名前は設定ファイル **config-`<instance>`.xml** の生成に使用され、コマンドラインパラメーターでインスタンスを識別するために使用されるので、必ず特殊文字のない短い名前を選択してください。 例：**eMarketing**。

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は 40 文字以下にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、メッセージがスパムと見なされるのを防ぐことができます。特に、SpamAssassin などのツールを使用します。

1. **[!UICONTROL DNS マスク]** フィールドに、インスタンスを接続する DNS マスクの **リスト** を入力します。 Adobe Campaignサーバーは、HTTP 要求に表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は、文字列 **https://** と、サーバーアドレスの先頭のスラッシュ文字 **/** の間に含まれます。

   値のリストをコンマで区切って定義できます。

    ? および*文字をワイルドカードとして使用して、1 つまたは様々な文字（DNS、ポートなど）を置き換えることができます。 例えば、**demo*** 値は「https://demo」と同じように「https://demo:8080」と「https://demo2」とも連携します。

   使用する名前は DNS で定義する必要があります。 Windows の場合は **c:/windows/system32/drivers/etc/hosts** ファイル、Linux の場合は **/etc/hosts** ファイルで、DNS 名と IP アドレスの対応を通知することもできます。 したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   サーバーは、特に E メールで画像をアップロードする場合は、この名前で識別する必要があります。

   さらに、サーバは、この名前で自身に接続できる必要があります。また、ループバックアドレス (127.0.0.1) で接続できる場合は、特にPDF形式でレポートを書き出せるようにする必要があります。

1. 「**[!UICONTROL 言語]**」ドロップダウンリストで、**インスタンスの言語** を選択します。英語（米国）、英語（英国）、フランス語、日本語。

   英語と英語の違いについては、[ この節 ](../../platform/using/adobe-campaign-workspace.md#date-and-time) で説明します。

   >[!CAUTION]
   >
   >この手順の後は、インスタンスの言語を変更できません。 Adobe Campaignインスタンスは多言語ではありません。インターフェイスを言語から別の言語に切り替えることはできません。

1. 「**[!UICONTROL OK]**」をクリックして、インスタンスの宣言を確定します。 ログオフし、ログオンし直して、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスは、コマンドラインから作成できます。 詳しくは、[ コマンドライン ](../../installation/using/command-lines.md) を参照してください。
