---
product: campaign
title: インスタンスの作成とログオン
description: インスタンスの作成とログオン
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 8%

---

# インスタンスの作成とログオン{#creating-an-instance-and-logging-on}



新しいインスタンスとAdobe Campaign データベースを作成するには、次の手順に従います。

1. 接続を作成します。
1. ログオンして関連インスタンスを作成します。
1. データベース作成および設定します。

>[!NOTE]
>
>これらの操作を実行できるのは、 **内部** 識別子のみです。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaign コンソールが起動したら、ログイン ページにアクセスします。

新しいインスタンスを作成するには、次の手順に従いますフォローする。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続構成ウィンドウにアクセスします。 このリンクは、**[!UICONTROL 新規…]** または既存のインスタンス名のいずれかです。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、`https://<machine>.<domain>.com` タイプの URL を使用できます。

   >[!CAUTION]
   >
   >接続URLには、 `[a-z]`、 `[A-Z]`、 `[0-9]` 、ダッシュ (-) または終止符の文字のみを使用します。

1. **[!UICONTROL OK]**&#x200B;をクリックして設定を確認します:これで、インスタンス作成プロセスを開始できます。
1. **[!UICONTROL 接続設定]**&#x200B;ウィンドウで、**内部** ログインとそのパスワードを入力して、Adobe Campaign アプリケーションサーバーに接続します。接続したら、インスタンス作成アシスタントにアクセスして新しいインスタンスを宣言します
1. [ **[!UICONTROL 名前]** ] フィールドに、 **インスタンス名**&#x200B;を入力します。 この名前は設定ファイル **config-`<instance>`.xml** の生成に使用され、インスタンスを識別するためにコマンドラインパラメータで使用されるため、特殊文字を含まない短い名前を選択してください。 例: **eMarketing**。

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は、40 文字以下にする必要があります。 これにより、「メッセージ-ID」ヘッダーのサイズを制限し、特にSpamAssassinなどのツールによってメッセージがスパムと見なされるのを防ぐことができます。

1. [**[!UICONTROL DNS マスク]** フィールドに、インスタンスをアタッチする DNS マスク&#x200B;****&#x200B;リストを入力します。Adobe Campaign サーバーは、HTTP リクエストに表示されるホスト名を使用して、到達するインスタンスを判断します。

   ホスト名は、文字列 **https://** とサーバーアドレスの最初のスラッシュ文字 **/** の間に含まれます。

   コンマで区切られた値のリストを定義できます。

   は？ また、 &#42; 文字をワイルドカードとして使用して、1つまたは複数の文字(DNS、ポートなど)を置き換えることができます。 インスタンス の場合、 **demo&#42;** 値は、「https://demo:8080」と「https://demo2」の場合と同様に、「https://demo」均等機能します。

   使用する名前は、DNS で定義されている必要があります。 また、DNS 名と IP アドレスの対応を、Windows では **c:/windows/system32/drivers/etc/hosts** ファイル、Linux では **/etc/hosts** ファイルで通知することもできます。 したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   サーバーは、特に電子メールで画像をアップロードする場合、この名前で識別される必要があります。

   さらに、サーバーは、特にレポートを PDF 形式でエクスポートできるようにするために、この名前で、可能であればループバック アドレス (127.0.0.1) で自身に接続できる必要があります。

1. **[!UICONTROL 言語]** ドロップダウン リストで、**インスタンス言語として 英語 (米国)、英語 (英国)、フランス語、または日本語** を選択します。

   アメリカ英語とイギリス英語の違いについては [ この節 ](../../platform/using/adobe-campaign-workspace.md#date-and-time) で説明します。

   >[!CAUTION]
   >
   >この手順の後でインスタンスの言語を変更することはできません。 Adobe Campaign インスタンスは多言語ではありません。インターフェイスを言語から別の言語に切り替えることはできません。

1. **[!UICONTROL OK]** をクリックして、インスタンスの宣言を確認します。 ログオフしてから再度ログオンし、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスはコマンドラインから作成できます。 詳しくは、 [コマンド行](../../installation/using/command-lines.md)を参照してください。
