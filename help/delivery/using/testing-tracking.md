---
title: トラッキングのテスト
seo-title: トラッキングのテスト
description: トラッキングのテスト
seo-description: null
page-status-flag: never-activated
uuid: 76d84ab4-b632-4498-96a1-ce9c773ec125
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: tracking-messages
discoiquuid: 4ed23249-4ecf-4e57-91b3-6fae1387bd6a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# トラッキングのテスト{#testing-tracking}

ミラーページ、E メールログ、リンクのトラッキングをテストできます。手順は次のとおりです。

1. テストに使用する E メールの配信を新規作成します。
1. E メールを受信するユーザーを指定します。このユーザーは E メールを開いて中のリンクをクリックすることになるので、制御可能なテスト用受信者アドレスを選択するようにしてください。
1. ミラーページ（MirrorPage）パーソナライゼーションブロックを E メールのコンテンツに追加します。
1. リンクが含まれている配信をミラーページに送信します。
1. この E メールを受信したら、開いてミラーページのリンクをクリックします。
1. After you are correctly redirected to the mirror page, access the **Administration > Technical workflows** folder and open the **Tracking** workflow.
1. Start the workflow, right click the **Scheduler** activity and select **Execute pending task now**.
1. 約 30 秒待ってから、「**監査**」タブを選択します。少なくとも 1 つのトラッキングログレコードがあることを確認します。

   新しいログが表示されていない場合は、「**更新**」をクリックします。

1. テストに使用した受信者のプロファイルページを開き、「**トラッキング**」タブを選択します。一部のレコードでは、「**タイプ**」列の値が「**ミラーページ**」となっています。

   >[!NOTE]
   >
   >The recipient&#39;s profile page is located in the **Profiles and Targets > Recipients** folder by default.

   To check the email log tracking, look for the values **Open** and **[!UICONTROL Email click]** in the **Type** column.

   If the open logs do not appear, go to the delivery and access its **Properties** to make sure that both **Activate tracking** and **[!UICONTROL Opens tracking]** options are checked.

