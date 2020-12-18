---
solution: Campaign Classic
product: campaign
title: インスタンスの作成とログオン
description: インスタンスの作成とログオン
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 3%

---


# インスタンスの作成とログオン{#creating-an-instance-and-logging-on}

新しいインスタンスとAdobe Campaign・データベースを作成するには、次のプロセスを適用します。

1. 接続を作成します。
1. ログオンして、関連するインスタンスを作成します。
1. データベースを作成し、設定します。

>[!NOTE]
>
>これらの操作を実行できるのは、**内部**&#x200B;識別子だけです。 詳しくは、[内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

Adobe Campaignコンソールを起動すると、ログインページにアクセスします。

新しいインスタンスを作成するには、次の手順に従います。

1. 秘密鍵証明書フィールドの右上隅にあるリンクをクリックして、接続設定ウィンドウにアクセスします。 このリンクは&#x200B;**[!UICONTROL 新規…]**&#x200B;または既存のインスタンス名。

   ![](assets/s_ncs_install_define_connection_01.png)

1. **[!UICONTROL 追加/Connection]**&#x200B;をクリックし、Adobe CampaignアプリケーションサーバーのラベルとURLを入力します。

   ![](assets/s_ncs_install_define_connection_02.png)

1. URLを介したAdobe Campaignアプリケーションサーバーへの接続を指定します。 DNS、マシンのエイリアス、またはIPアドレスを使用します。

   例えば、[`https://<machine>.<domain>.com`](https://myserver.adobe.com)タイプURLを使用できます。

   >[!CAUTION]
   >
   >接続URLには、次の文字のみを使用します。`[a-z]`、`[A-Z]`、`[0-9]`、ダッシュ(-)、またはフルストップ。

1. 「**[!UICONTROL OK]**」をクリックして設定を確認します。これで、インスタンス作成プロセスから開始できます。
1. **[!UICONTROL Adobe Campaign設定]**&#x200B;ウィンドウで、**内部**&#x200B;ログインとパスワードを入力し、接続アプリケーションサーバーに接続します。 接続が完了したら、インスタンス作成ウィザードにアクセスして新しいインスタンスを宣言します
1. 「**[!UICONTROL 名前]**」フィールドに、**インスタンス名**&#x200B;を入力します。 この名前は設定ファイル&#x200B;**config-`<instance>`.xml**&#x200B;の生成に使用され、コマンドラインパラメーターでインスタンスを識別するために使用されるので、必ず特殊文字を含まない短い名前を選択してください。 次に例を示します。**eMarketing**。

   ![](assets/s_ncs_install_create_instance.png)

   ドメイン名に追加するインスタンスの名前は40文字以下にする必要があります。 これにより、「Message-ID」ヘッダーのサイズを制限し、特にSpamAssicinなどのツールでメッセージがスパムと見なされるのを防ぐことができます。

1. **[!UICONTROL DNSマスク]**&#x200B;フィールドに、インスタンスをアタッチするDNSマスク&#x200B;**の**&#x200B;リストを入力します。 Adobe Campaignサーバーは、HTTPリクエストに表示されるホスト名を使用して、到達するインスタンスを決定します。

   ホスト名は、文字列&#x200B;**https://**&#x200B;と、サーバーアドレスの先頭のスラッシュ文字&#x200B;**/**&#x200B;の間に含まれます。

   値のリストをカンマで区切って定義できます。

    ? また、1つまたは複数の文字（DNS、ポートなど）を置き換える場合は、ワイルドカードとして*文字を使用できます。 例えば、**demo***&#x200B;値は&quot;https://demo&quot;と共に使用でき、&quot;https://demo:8080&quot;と共に&quot;https://demo2&quot;とも使用できます。

   使用する名前は、DNSで定義する必要があります。 また、Windowsの&#x200B;**c:/windows/system32/drivers/etc/hosts**&#x200B;ファイルと、Linuxの&#x200B;**/etc/hosts**&#x200B;ファイル内のDNS名とIPアドレスとの通信を通知することもできます。 したがって、選択したインスタンスに接続するには、このDNS名を使用するように接続設定を変更する必要があります。

   サーバーは、特に電子メールで画像をアップロードする場合、この名前で識別する必要があります。

   さらに、サーバはこの名前で自身に接続でき、可能であればループバックアドレス127.0.0.1で接続できる必要があります。特に、レポートをPDF形式でエクスポートできるようにするためです。

1. **[!UICONTROL 言語]**&#x200B;ドロップダウンリストで、**インスタンス言語**&#x200B;を選択します。英語（米国）、英語（英国）、フランス語または日本語。

   英語と英語の違いについては、[このセクション](../../platform/using/adobe-campaign-workspace.md#date-and-time)で説明します。

   >[!CAUTION]
   >
   >この手順の後でインスタンス言語を変更することはできません。 Adobe Campaignインスタンスが多言語ではありません：インターフェイスを言語から別の言語に切り替えることはできません。

1. 「**[!UICONTROL OK]**」をクリックして、インスタンスの宣言を確定します。 ログオフしてから再度ログオンし、データベースを宣言します。

   >[!NOTE]
   >
   >インスタンスは、コマンドラインから作成できます。 詳しくは、[コマンドライン](../../installation/using/command-lines.md)を参照してください。

