---
solution: Campaign Classic
product: campaign
title: Adobe Campaign の起動
description: Adobe Campaign の起動
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
translation-type: tm+mt
source-git-commit: b77a56a97e499f60c092fae45c7809f7bfd9f2ea
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 98%

---


# Adobe Campaign の起動{#launching-adobe-campaign}

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。[このページ](../../installation/using/installing-the-client-console.md)では、クライアントコンソールをダウンロードして設定する方法を説明します。

## Adobe Campaign の起動 {#starting-adobe-campaign}

Adobe Campaign を起動するには、**[!UICONTROL スタート／すべてのプログラム／Adobe Campaign v.X／Adobe Campaign クライアントコンソール]**&#x200B;を選択します。

クライアントコンソール接続ウィンドウで、既存のデータベースを選択するか設定し、ユーザー名およびパスワードを使用してデータベースに接続できます。

![](assets/acc-logon.png)

## Adobe Campaign への接続 {#connecting-to-adobe-campaign}

Adobe ID を使用して Adobe Campaign に接続できます。詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。

専用のログイン／パスワードを使用して接続することもできます。

1. 「**[!UICONTROL ログイン]**」フィールドに、オペレーターのアカウント ID を入力します。

   ID は、Adobe Campaign プラットフォームの管理者から付与されます。

1. 「**[!UICONTROL パスワード]**」フィールドにパスワードを入力します。

   データベースに最初にアクセスする際のパスワードは、管理者が指定したものになります。接続すると、**[!UICONTROL ツール／パスワードを変更...]** メニューからパスワードを変更できます。オペレーターおよび接続について詳しくは、[アクセス管理](../../platform/using/access-management.md)を参照してください。

1. 「**[!UICONTROL ログイン]**」をクリックして確定します。<!--You can also press the **Enter** key to launch connection.-->

これで、[Adobe Campaign ワークスペース](../../platform/using/adobe-campaign-workspace.md)にアクセスできるようになります。

**[!UICONTROL ログイン画面]**&#x200B;では、次のキーボードショートカットが利用できます。
* すべてのアクション可能な項目は、**Tab** キー（上から下）または **Tab** + **Shift** キー（下から上）で選択できます。
* 接続を開始するには、**Enter** キーを押すこともできます。
* **Esc** キーを使用すると、「**[!UICONTROL ログイン]**」フィールドと「**[!UICONTROL パスワード]**」フィールドを、最後に成功した接続値にリセットできます。

## 接続の設定 {#setting-up-connections}

入力ゾーンの上にあるリンクから、サーバー接続設定にアクセスできます。

![](assets/s_ncs_user_connections_management.png)

**[!UICONTROL 接続]**&#x200B;ウィンドウで、**[!UICONTROL 追加／接続]**&#x200B;をクリックします。

次に、接続設定を定義する必要があります。手順は次のとおりです。

1. 「**[!UICONTROL ラベル]**」を入力して、データベース接続に名前を割り当てます。

1. 「**[!UICONTROL URL]**」フィールドで、アプリケーションサーバーのアドレスを追加します。接続 URL が不明な場合は、管理者にお問い合わせください。

1. オペレーターが Adobe ID を使用してコンソールに接続するには、「**[!UICONTROL Adobe ID を使用して接続]**」をオンにします。詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。

1. 「**[!UICONTROL OK]**」をクリックして検証します。

## オペレーターと権限 {#operators-and-permissions}

ソフトウェアにアクセスできるオペレーターの識別子とパスワードおよびそれぞれの権限は、Adobe Campaign システム管理者が Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／アクセス管理／オペレーター]**&#x200B;ノードで定義します。

この機能について詳しくは、[アクセス管理](../../platform/using/access-management.md)の節で説明しています。

## Adobe Campaign からの切断 {#disconnecting-from-adobe-campaign}

Adobe Campaign から切断するには、アイコンバーの最初のアイコンを使用します。

![](assets/s_ncs_user_deconnexion.png)

>[!NOTE]
>
>ログオフしないでアプリケーションを閉じることもできます。

## Adobe Campaign のバージョンの確認 {#getting-your-campaign-version}

**[!UICONTROL ヘルプ／バージョン情報...]** メニューから、次の情報にアクセスできます。

* Campaign のクライアントコンソールとアプリケーションサーバーの&#x200B;**バージョン**&#x200B;番号
* Campaign のクライアントコンソールとアプリケーションサーバーの&#x200B;**ビルド**&#x200B;番号
* アドビカスタマーサポートに連絡するためのリンク
* アドビのプライバシーポリシー、利用条件、Cookie ポリシーへのリンク

![](assets/about-acc.png)

アドビのカスタマーサポートチームに連絡する場合は、Adobe Campaign クライアントコンソールおよびアプリケーションサーバーのバージョン番号とビルド番号を伝える必要があります。

[ [!DNL Gold Standard] Campaign バージョン](../../rn/using/gold-standard.md)を実行している場合は、「**[!UICONTROL バージョン情報]**」ボックスに表示される SHA/1 文字も共有する必要があります。例えば、Gold **Standard 10 リリース**&#x200B;の場合、ビルド番号は次のように **build 9032@efd8a94** と表示されます。

![](assets/about-acc-gs.png)

[!DNL Gold Standard] [の詳細については、この記事](../../rn/using/gs-overview.md)を参照してください。

**関連トピック**：

* [Adobe Campaign のヘルプとサポートのオプション](https://helpx.adobe.com/jp/campaign/kb/ac-support.html)
* [Adobe Campaign ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)
* [Adobe Experience Cloud のサポートおよびエキスパートセッション](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
