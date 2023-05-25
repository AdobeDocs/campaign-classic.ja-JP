---
product: campaign
title: Adobe Campaign のローンチ
description: Adobe Campaign のローンチ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 4d9c5b24-83a2-4495-a56c-5bc376d69703
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Adobe Campaign のローンチ{#launching-adobe-campaign}



Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。[このページ](../../installation/using/installing-the-client-console.md)では、クライアントコンソールをダウンロードして設定する方法を説明します。

>[!CAUTION]
>
>お使いのシステムおよびツールと Adobe Campaign クライアントコンソールの互換性を確認するには、[互換性マトリックス](../../rn/using/compatibility-matrix.md#ClientConsoleoperatingsystems)を参照してください。

## Adobe Campaign の利用開始 {#starting-adobe-campaign}

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

**関連トピック**：

* [Adobe Campaign のヘルプとサポートのオプション](../../support.md)
* [Adobe Campaign ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)
* [Adobe Experience Cloud のサポートおよびエキスパートセッション](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
