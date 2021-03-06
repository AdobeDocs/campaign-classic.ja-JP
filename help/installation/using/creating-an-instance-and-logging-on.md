---
product: campaign
title: インスタンスの作成とログイン
description: インスタンスの作成とログイン
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: f4513834cf721f6d962c7c02c6c64b2171059352
workflow-type: tm+mt
source-wordcount: '598'
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
>次の項目のみ **内部** 識別子は、これらの操作を実行できます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaignコンソールを起動したら、ログインページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。このリンクは、 **[!UICONTROL 新規…]** または既存のインスタンス名

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、`https://<machine>.<domain>.com` タイプの URL を使用できます。

   >[!CAUTION]
   >
   >接続 URL には、次の文字のみを使用します。 `[a-z]`, `[A-Z]`, `[0-9]` ダッシュ (-) またはフルストップ

1. クリック **[!UICONTROL Ok]** 設定を確認するには：これで、インスタンス作成プロセスから始めることができます。
1. 内 **[!UICONTROL 接続設定]** ウィンドウで、 **内部** Adobe Campaignアプリケーションサーバーに接続するためのログインとパスワード。 接続したら、インスタンス作成ウィザードにアクセスして、新しいインスタンスを宣言します
1. 内 **[!UICONTROL 名前]** フィールドに、 **インスタンス名**. この名前は設定ファイルの生成に使用されるので、 **config-`<instance>`.xml** およびは、インスタンスを識別するためにコマンドラインパラメーターで使用されます。必ず、特殊文字のない短い名前を選択してください。 例： **eMarketing**.

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は 40 文字以内にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、特に SpamAssassin などのツールによってメッセージがスパムと見なされるのを防ぐことができます。

1. 内 **[!UICONTROL DNS マスク]** フィールドに、 **DNS マスクのリスト** インスタンスを添付する先に。 Adobe Campaignサーバーは、HTTP リクエストに表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は文字列の間に含まれます **https://** 最初のスラッシュ文字 **/** を設定します。

   値のリストをコンマで区切って定義できます。

   null ? および &#42; 文字をワイルドカードとして使用して、1 つまたは様々な文字（DNS、ポートなど）を置き換えることができます。 例えば、 **デモ&#42;** 値は「https://demo」と「https://demo:8080」と「https://demo2」と同様に機能します。

   使用する名前は DNS で定義する必要があります。 また、DNS 名と IP アドレスの間の通信を **c:/windows/system32/drivers/etc/hosts** Windows と **/etc/hosts** ファイルに含まれています。 したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   サーバーは、特に E メールで画像をアップロードする場合に、この名前で識別する必要があります。

   さらに、サーバは、この名前で自身に接続でき、可能であればループバックアドレス (127.0.0.1) で接続できる必要があります。特に、PDF形式でレポートを書き出せるようにする必要があります。

1. 内 **[!UICONTROL 言語]** ドロップダウンリストから、 **インスタンス言語**:英語（米国）、英語（英国）、フランス語、日本語。

   米国英語と英国英語の違いについては、 [この節](../../platform/using/adobe-campaign-workspace.md#date-and-time).

   >[!CAUTION]
   >
   >この手順の後は、インスタンスの言語を変更できません。 Adobe Campaignインスタンスは多言語ではありません：インターフェイスを言語から別の言語に切り替えることはできません。

1. クリック **[!UICONTROL Ok]** をクリックして、インスタンスの宣言を確定します。 ログオフし、再度ログオンして、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスは、コマンドラインから作成できます。 詳しくは、 [コマンドライン](../../installation/using/command-lines.md).
