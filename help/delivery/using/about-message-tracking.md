---
solution: Campaign Classic
product: campaign
title: 追跡の概要
description: Adobe Campaign Classicでの追跡に関する一般的なガイドラインを参照してください。
audience: delivery
content-type: reference
topic-tags: tracking-messages
translation-type: tm+mt
source-git-commit: 55cc09c0446e389029890e45b790bb5ec6ffdc27
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 22%

---


# メッセージ追跡の開始{#get-started-tracking}

Adobe Campaignでは、その追跡機能のおかげで、送信されたメッセージを追跡し、受信者の動作を確認することができます。開く、リンクのクリック、購読解除など

この情報は、配信の各受信者のプロファイルの&#x200B;**[!UICONTROL 「追跡]**」タブで取得されます。 このタブには、リストから選択した受信者がトラッキングおよびクリックしたすべての URL が表示されます。これは、配信画面に現在も表示されている配信内でトラッキングされたすべての URL の累積です。このリストは設定可能で、一般的には、クリックされた URL、クリックの日時、URL が含まれていたドキュメントが表示されます。詳しくは、[この節](../../platform/using/editing-a-profile.md#tracking-tab)を参照してください。

**配信ダッシュボード**&#x200B;は、配信の監視や、メッセージの送信中に発生する最終的な問題を監視するための重要な要素です。 詳しくは[この節](../../delivery/using/delivery-dashboard.md)を参照してください。

次の図に、ユーザーと様々なサーバー間のダイアログのステージを示します。

![](assets/tracking-diagram.png)

## 追跡を設定{#configure-tracking}

<img src="assets/do-not-localize/icon-configure.svg" width="60px">

**動作の仕組み**

トラッキングを使用する前に、まずインスタンスに対して設定する必要があります。 [詳細情報](../../installation/using/deploying-an-instance.md#operating-principle)

**トラッキングサーバー**

トラッキングを設定するには、インスタンスを宣言し、トラッキングサーバーに登録する必要があります。 [詳細情報](../../installation/using/deploying-an-instance.md#tracking-server)

**トラッキングの保存**

追跡を設定し、URLを入力したら、追跡サーバーを登録する必要があります。 [詳細情報](../../installation/using/deploying-an-instance.md#tracking-configuration#saving-tracking)

## メッセージトラッキング {#message-tracking}

<img src="assets/do-not-localize/icon-message-tracking.svg" width="60px">

**追跡されたリンク**

メッセージの受信、およびメッセージコンテンツに挿入されたリンクのアクティベーションを追跡し、受信者の動作をより深く把握できます。 [詳細情報](../../delivery/using/how-to-configure-tracked-links.md)

**URL追跡**

追跡オプションは、追跡するURLをアクティブ化または非アクティブ化することで設定できます。 [詳細情報](../../delivery/using/personalizing-url-tracking.md)

**追跡されるリンクのパーソナライゼーション**

Campaign Classicトラッキング機能を使用すると、パーソナライズ可能な電子メールにリンクを追加し、トラッキングをサポートできます。 [詳細情報](https://helpx.adobe.com/campaign/kb/tracking-personnalized-links.html)

**トラッキングログ**

配信が送信され、トラッキングがアクティブ化されると、トラッキングテクニカルワークフローはトラッキングデータを取得します。 このデータは、配信の「追跡」タブにあります。 [詳細情報](../../delivery/using/accessing-the-tracking-logs.md)

**トラッキングのテスト**

追跡用のメッセージを送信する前に、ミラーページ、電子メールログ、リンクで追跡をテストできます。 [詳細情報](../../delivery/using/testing-tracking.md)

## Web アプリケーショントラッキング {#web-application-tracking}

<img src="assets/do-not-localize/icon-web-app.svg" width="60px">

**Web アプリケーションのトラッキング**

また、トラッキングタグを含むWeb アプリケーションページの訪問を追跡および測定できます。 この機能は、フォームやオンライン調査など、すべての種類のWeb アプリケーションで使用できます。 [詳細情報](../../web/using/tracking-a-web-application.md)

**Web アプリケーショントラッキングのオプトアウト**

Web アプリケーション追跡オプトアウトを使用すると、行動追跡をオプトアウトしたエンドユーザーのWeb行動の追跡を停止できます。 Webアプリケーションやランディングページにバナーを表示して、ユーザーがオプトアウトできるようにする機能を追加できます。 [詳細情報](../../web/using/web-application-tracking-opt-out.md)

## 追跡レポート{#tracking-reports}

<img src="assets/do-not-localize/icon_monitor.svg" width="60px">

**トラッキング統計**

このレポートは、開封数、クリック数、トランザクション数に関する統計を提供し、配信のマーケティングインパクトを追跡できます。 [詳細情報](../../reporting/using/delivery-reports.md#tracking-statistics)

**URL とクリックストリーム**

このレポートは、配信後に訪問されたページのリストを表示します。[詳細情報](../../reporting/using/delivery-reports.md#urls-and-click-streams)

**人／ユーザーと受信者**

この例にAdobe Campaignして、人/人と受信者のトラッキングの違いをより深く理解します。 [詳細情報](../../reporting/using/person-people-recipients.md)

**トラッキング指標**

このレポートは、開いた受信者、クリックスルー率、クリックストリームなどの配信を受け取ったときの訪問者の行動を追跡する主要指標を組み合わせたものです。 [詳細情報](../../reporting/using/delivery-reports.md#tracking-indicators)

**指標の計算**

各表には、様々なレポートで使用されるインジケータのリストと、配信タイプに応じたその計算式が示されます。 [詳細情報](../../reporting/using/indicator-calculation.md)

## トラッキングのトラブルシューティング{#tracking-troubleshooting}

<img src="assets/do-not-localize/icon-troubleshooting.svg" width="60px">

以下のトラブルシューティングのヒントは、Adobe Campaign Classicでトラッキングを使用する場合に発生する最も一般的な問題の解決に役立ちます。 より高度なトラブルシューティングについては、[この](../../delivery/using/tracking-troubleshooting.md)を参照してください。

* trackinglogdプロセスが実行中であることを確認します

   このプロセスは、IIS/Webサーバーの共有メモリから読み取り、リダイレクトログを書き込みます。

   ホームページからアクセスするには、インスタンスの[監視]タブを選択します。 また、インスタンスで次のコマンドを実行することもできます。`<user>@<instance>:~$ nlserver pdump`

   trackinglogdプロセスがリストに表示されない場合は、インスタンスで次のコマンドを使用して起動します。`<user>@<instance>:~$ nlserver start trackinglogd`

* トラッキングテクニカルワークフローが最近実行されていることを確認します。

   トラッキングのテクニカルワークフローは、テクニカルワークフロー/運用/フォルダーで確認できます。
