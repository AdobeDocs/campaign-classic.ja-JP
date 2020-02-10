---
title: SpamAssassin
seo-title: SpamAssassin
description: SpamAssassin
seo-description: null
page-status-flag: never-activated
uuid: 4f439432-4215-42ed-8f92-b4ca8dd92726
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: d41658ab-ee79-4a5c-a165-d94b81eb2b33
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# SpamAssassin{#spamassassin}

## SpamAssassin について {#about-spamassassin}

Adobe Campaign は、E メールスパムフィルタリングに使用されるサードパーティのサービスである、[SpamAssassin](https://spamassassin.apache.org) と連携するように設定できます。これを使用すると、E メールを採点して、受信時に使用されるスパム対策ツールによってメッセージがスパムとみなされるリスクがあるかどうかを判断できます。

SpamAssassin は、次のような様々なスパム検出技法を活用します。

* DNS ベースおよびファジーチェックサムベースのスパム検出
* ベイジアンフィルタリング
* 外部プログラム
* ブラックリスト
* オンラインデータベース

>[!NOTE]
>
>SpamAssassin は、Adobe Campaign アプリケーションサーバーにインストールして、設定する必要があります。詳しくは、[この節](../../installation/using/configuring-spamassassin.md)を参照してください。
>
>要素がスパムかどうかを左右するルールは、SpamAssassin で管理され、権限を持つ管理者が編集できます。

## SpamAssassin の使用 {#using-spamassassin}

E メール配信を作成して、そのコンテンツを定義したら、以下の手順に従って、リスクを評価します。

配信の作成およびデザインについて詳しくは、[この節](../../delivery/using/about-email-channel.md)を参照してください。

1. Go to the **[!UICONTROL Preview]** tab.
1. 配信をプレビューする受信者を選択します。

   ![](assets/s_tn_del_preview_spamassassin_recipient.png)

   >[!NOTE]
   >
   >受信者を選択しないと、スパム対策チェックは実行できません。

1. テストの結果が警告メッセージとして表示されます。高レベルのリスクが検出された場合、次の警告メッセージが表示されます。

   ![](assets/s_tn_del_preview_spamassassin_ko.png)

1. Click the **[!UICONTROL More...]** link next to the warning.
1. タブを選択 **[!UICONTROL Anti-spam checking]** します。
1. Go to the **[!UICONTROL Points / Rule / Description]** section to view the reasons for this risk.

   ![](assets/s_tn_del_msg_spamassassin_ko.png)

>[!NOTE]
>
>Each time you click the **[!UICONTROL Anti-spam checking]**, the SpamAssassin service is called and the message is analyzed again for anti-spam detection. コンテンツを変更してから、スパム対策分析を再実行するようにしてください。
