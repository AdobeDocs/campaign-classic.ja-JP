---
title: Adobe Campaign の起動
seo-title: Adobe Campaign の起動
description: Adobe Campaign の起動
seo-description: null
page-status-flag: never-activated
uuid: c1c5bb0d-ae8e-4b0e-ab39-8b2291162557
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 6652b081-66b6-47a8-97e5-383e3251647e
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 51e4d72abf3a1f48700ca38566dbf06dd24594b8

---


# Adobe Campaign の起動{#launching-adobe-campaign}

## Adobe Campaign の起動 {#starting-adobe-campaign}

Adobe Campaign を起動するには、**[!UICONTROL スタート／すべてのプログラム／Adobe Campaign v.X／Adobe Campaign クライアントコンソール]**&#x200B;を選択します。

クライアントコンソール接続ウィンドウで、既存のデータベースを選択するか設定し、ユーザー名およびパスワードを使用してデータベースに接続できます。

![](assets/s_ncs_user_login.png)

## Adobe Campaign への接続 {#connecting-to-adobe-campaign}

Adobe ID を使用して Adobe Campaign に接続できます。詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。

専用のログイン／パスワードを使用して接続することもできます。

1. 「**[!UICONTROL ログイン]**」フィールドに、オペレーターのアカウント ID を入力します。

   ID は、Adobe Campaign プラットフォームの管理者から付与されます。

1. 「**[!UICONTROL パスワード]**」フィールドにパスワードを入力します。

   データベースに最初にアクセスする際のパスワードは、管理者が指定したものになります。接続すると、**[!UICONTROL ツール／パスワードを変更...]** メニューからパスワードを変更できます。オペレーターおよび接続について詳しくは、[アクセス管理](../../platform/using/access-management.md)を参照してください。

1. 「**[!UICONTROL ログイン]**」をクリックして確定します。

これで、[Adobe Campaign ワークスペース](../../platform/using/adobe-campaign-workspace.md)にアクセスできるようになります。

## 接続の設定 {#setting-up-connections}

入力ゾーンの上にあるリンクから、サーバー接続設定にアクセスできます。

![](assets/s_ncs_user_connections_management.png)

**[!UICONTROL 接続]**&#x200B;ウィンドウで、**[!UICONTROL 追加／接続]**&#x200B;をクリックします。

![](assets/s_ncs_user_add_connexion.png)

次に、接続設定を定義する必要があります。手順は次のとおりです。

* 「**[!UICONTROL ラベル]**」を入力して、データベース接続に名前を割り当てます。
* 「**[!UICONTROL URL]**」フィールドで、アプリケーションサーバーのアドレスを追加します。接続 URL が不明な場合は、管理者にお問い合わせください。
* オペレーターが Adobe ID を使用してコンソールに接続するには、「**[!UICONTROL Adobe ID を使用して接続]**」をオンにします。詳しくは、[このページ](../../integrations/using/about-adobe-id.md)を参照してください。
* 「**[!UICONTROL OK]**」をクリックして検証します。

>[!NOTE]
>
>「**[!UICONTROL 追加]**」ボタンを使用すると、すべての接続を整理する&#x200B;**[!UICONTROL フォルダー]**&#x200B;を作成できます。各接続をフォルダーにドラッグ＆ドロップします。

## オペレーターと権限 {#operators-and-permissions}

ソフトウェアにアクセスできるオペレーターの識別子とパスワードおよびそれぞれの権限は、Adobe Campaign システム管理者が Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／アクセス管理／オペレーター]**&#x200B;ノードで定義します。

この機能について詳しくは、[アクセス管理](../../platform/using/access-management.md)の節で説明しています。

## Adobe Campaign からの切断 {#disconnecting-from-adobe-campaign}

Adobe Campaign から切断するには、アイコンバーの最初のアイコンを使用します。

![](assets/s_ncs_user_deconnexion.png)

>[!NOTE]
>
>ログオフしないでアプリケーションを閉じることもできます。

## Campaign のバージョンの確認 {#getting-your-campaign-version}

**[!UICONTROL ヘルプ／バージョン情報...]** メニューから、次の情報にアクセスできます。

* **バージョン**&#x200B;番号
* **ビルド**&#x200B;番号
* Adobe Campaign サポートに連絡するためのリンク

   >[!CAUTION]
   >
   >アドビサポートチームに連絡する場合は、Campaign クライアントコンソールおよびアプリケーションサーバーのバージョン番号とビルド番号を伝える必要があります。

