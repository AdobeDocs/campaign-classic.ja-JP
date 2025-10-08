---
product: campaign
title: インスタンスの作成とログオン
description: インスタンスの作成とログオン
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: c38150aa8de90f314e1f2a43c6751d4db4059533
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 9%

---

# インスタンスの作成とログオン{#creating-an-instance-and-logging-on}



新しいインスタンスとAdobe Campaign データベースを作成するには、次の手順に従います。

1. 接続を作成します。
1. ログオンして関連インスタンスを作成します。
1. データベースを作成し、設定します。

>[!NOTE]
>
>これらの操作を実行できるのは **内部** 識別子のみです。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaign コンソールが起動したら、ログインページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 資格情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。 このリンクは、**[!UICONTROL 新規…]** または既存のインスタンス名のいずれかです。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   例えば、`https://<machine>.<domain>.com` タイプの URL を使用できます。

   >[!CAUTION]
   >
   >接続 URL には、`[a-z]`、`[A-Z]`、`[0-9]`、ダッシュ（–）またはフルストップの文字のみを使用します。

1. **[!UICONTROL OK]** をクリックして、設定を確定します。これで、インスタンス作成プロセスを開始できます。
1. **[!UICONTROL Connection settings]** ウィンドウで、Adobe Campaign アプリケーションサーバーに接続するための **internal** ログインとパスワードを入力します。 接続したら、インスタンス作成アシスタントにアクセスして、新しいインスタンスを宣言します
1. 「**[!UICONTROL 名前]**」フィールドに「**インスタンス名**」と入力します。 この名前は、設定ファイル **config-`<instance>`.xml** の生成に使用され、インスタンスを識別するためにコマンドラインパラメーターで使用されるので、特殊文字を含まない短い名前を選択してください。 例：**eMarketing**。

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は、40 文字以下にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、特に SpamAssassin などのツールによってメッセージがスパムと見なされるのを防ぐことができます。

1. **[!UICONTROL DNS マスク]** フィールドに、インスタンスを添付する **DNS マスクのリスト** を入力します。 Adobe Campaign サーバーは、HTTP リクエストに表示されるホスト名を使用して、到達するインスタンスを判断します。

   ホスト名は、文字列 **https://** とサーバーアドレスの最初のスラッシュ文字 **/** の間に含まれます。

   コンマで区切られた値のリストを定義できます。

   は？ および &#42; 文字は、ワイルドカードとして使用して、1 つまたは様々な文字（DNS、ポートなど）を置き換えることができます。 例えば、**demo&#42;** 値は、「https://demo」と連携します（「https://demo:8080」、さらには「https://demo2」と連携する場合もあります）。

   使用する名前は、DNS で定義する必要があります。 また、Windows の場合は **c:/windows/system32/drivers/etc/hosts** ファイルで、Linux の場合は **/etc/hosts** ファイルで、DNS 名と IP アドレスの対応を示すこともできます。 したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   特にメール内の画像をアップロードする場合、サーバーはこの名前で識別される必要があります。

   さらに、サーバは、この名前で、可能であればループバック アドレス（127.0.0.1）を使用して自分自身に接続できる必要があります。特に、レポートをPDF フォーマットでエクスポートできるようにするためです。

1. 「**[!UICONTROL 言語]**」ドロップダウンリストで、**インスタンス言語** として英語（米国）、英語（英国）、フランス語、日本語のいずれかを選択します。

   アメリカ英語とイギリス英語の違いについては、[Campaign v8 （コンソール）ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui) を参照してください。

   >[!CAUTION]
   >
   >この手順の後でインスタンスの言語を変更することはできません。 Adobe Campaign インスタンスは多言語ではありません。インターフェイスを言語から別の言語に切り替えることはできません。

1. **[!UICONTROL OK]** をクリックして、インスタンスの宣言を確認します。 ログオフしてから再度ログオンし、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスはコマンドラインから作成できます。 詳しくは、[ コマンドライン ](../../installation/using/command-lines.md) を参照してください。
