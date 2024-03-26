---
product: campaign
title: インスタンスの作成とログオン
description: インスタンスの作成とログオン
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a025026e-688e-4ec1-abc4-40ee040d2b3b
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 9%

---

# インスタンスの作成とログオン{#creating-an-instance-and-logging-on}



新しい インスタンス and Adobe Campaign データベースを作成するには、次の手順に従います。

1. 接続作成します。
1. ログオンして関連インスタンスを作成します。
1. データベース作成および設定します。

>[!NOTE]
>
>**内部**&#x200B;識別子のみがこれらの操作を実行できます。詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

Adobe Campaign コンソールが起動したら、ログイン ページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 認証情報フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。 このリンクは、 **[!UICONTROL 新規…]** または既存のインスタンス名

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加／接続]**&#x200B;をクリックし、Adobe Campaign アプリケーションサーバーのラベルと URL を入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URL 経由で Adobe Campaign アプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、または IP アドレスを使用します。

   たとえば、タイプ URL を使用できます `https://<machine>.<domain>.com` 。

   >[!CAUTION]
   >
   >接続URLには、ダッシュ (-) または終止符の文字`[a-z]``[A-Z]``[0-9]`のみを使用します。

1. [OK ]**]**[!UICONTROL &#x200B;をクリックして設定を確認します。これで、インスタンス作成プロセスを開始できます。
1. **[!UICONTROL 接続設定]**&#x200B;ウィンドウで、Adobe Campaign アプリケーションサーバーに接続するための内部&#x200B;**ログインとそのパスワードを入力します**。接続したら、インスタンス作成ウィザードにアクセスして新しいインスタンスを宣言します
1. [**[!UICONTROL 名前]**] フィールドに、インスタンス名を入力します。****&#x200B;この名前は設定ファイルの **config-`<instance>`.xml** を生成するために使用され、インスタンスを識別するためにコマンドラインパラメータで使用されるため、特殊文字を含まない短い名前を選択してください。 例： **eMarketing**.

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は 40 文字以内にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、特に SpamAssassin などのツールによってメッセージがスパムと見なされるのを防ぐことができます。

1. Adobe Analytics の **[!UICONTROL DNS マスク]** フィールドに、 **DNS マスクのリスト** インスタンスを添付する先のインスタンス。 Adobe Campaignサーバーは、HTTP リクエストに表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は文字列の間に含まれます **https://** 最初のスラッシュ文字 **/** の名前を指定します。

   カンマで区切られた値リストを定義できます。

   この ? また &#42; 、文字をワイルドカードとして使用して、1 文字または様々な文字(DNS、ポート など)を置き換えることができます。 インスタンスの場合、 **デモ&#42;** 値は「https://demo」でも「https://demo:8080」と「https://demo2」と同じように均等機能します。

   使用する名前は、DNS で定義されている必要があります。 また、DNS 名と IP アドレスの対応については、 **Windows の c:/windows/system32/drivers/etc/hosts** ファイルおよび **Linux の /etc/hosts** ファイルで通知することもできます。 したがって、選択したインスタンスに接続するには、この DNS 名を使用するように接続設定を変更する必要があります。

   サーバーは、特に電子メールで画像をアップロードする場合、この名前で識別される必要があります。

   さらに、サーバは、この名前で自身に接続でき、可能であればループバックアドレス (127.0.0.1) で接続できる必要があります。特に、PDF形式でレポートを書き出せるようにする必要があります。

1. Adobe Analytics の **[!UICONTROL 言語]** ドロップダウンリストから、 **インスタンス言語**：英語（米国）、英語（英国）、フランス語、日本語。

   英語（米国）と英語（英国）の違いについては、 [この節](../../platform/using/adobe-campaign-workspace.md#date-and-time).

   >[!CAUTION]
   >
   >この手順の後は、インスタンスの言語を変更できません。 Adobe Campaignインスタンスは多言語ではありません。インターフェイスを言語から別の言語に切り替えることはできません。

1. [OK]]**をクリックして**[!UICONTROL &#x200B;インスタンス宣言を確定します。ログオフしてから再度ログオンして、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスはコマンドラインから作成できます。 詳しくは、コマンド行](../../installation/using/command-lines.md)を参照してください[。
