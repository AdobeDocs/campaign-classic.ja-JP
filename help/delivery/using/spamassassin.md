---
product: campaign
title: SpamAssassin
description: SpamAssassin を使用したメールスパム検出の設定方法を説明します。
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Email, Deliverability
role: User
exl-id: 8be6836d-f7dc-4199-b2b2-b6a9cac9d162
TQID: https://experienceleague.adobe.com/nZB19N90xSjDCNnibtwcPBm75SSyxkq1hQxICXCOg2A
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 284
ht-degree: 100%

---

# SpamAssassin{#spamassassin}

Adobe Campaign は、メールスパムフィルタリングに使用されるサードパーティのサービスである、[SpamAssassin](https://spamassassin.apache.org) と連携するように設定できます。 これを使用すると、メールを採点して、受信時に使用されるスパム対策ツールによってメッセージがスパムとみなされるリスクがあるかどうかを判断できます。

SpamAssassin は、次のような様々なスパム検出技法を活用します。

* DNS ベースおよびファジーチェックサムベースのスパム検出
* ベイジアンフィルタリング
* 外部プログラム
* ブロックリスト
* オンラインデータベース

>[!NOTE]
>
>SpamAssassin は、Adobe Campaign アプリケーションサーバーにインストールして、設定する必要があります。 詳しくは、[この節](../../installation/using/configuring-spamassassin.md)を参照してください。
>
>要素がスパムかどうかを左右するルールは、SpamAssassin で管理され、権限を持つ管理者が編集できます。

## Campaign での SpamAssassin の使用 {#using-spamassassin}

メール配信を作成して、そのコンテンツを定義したら、以下の手順に従って、リスクを評価します。

配信の作成およびデザインについて詳しくは、[この節](about-email-channel.md)を参照してください。

1. 「**[!UICONTROL プレビュー]**」タブに移動します。
1. 配信をプレビューする受信者を選択します。

   ![](assets/s_tn_del_preview_spamassassin_recipient.png)

   >[!NOTE]
   >
   >受信者を選択しないと、スパム対策チェックは実行できません。

1. テストの結果が警告メッセージとして表示されます。 高レベルのリスクが検出された場合、次の警告メッセージが表示されます。

   ![](assets/s_tn_del_preview_spamassassin_ko.png)

1. 警告の隣にある&#x200B;**[!UICONTROL 詳細...]** リンクをクリックします。
1. 「**[!UICONTROL スパム対策チェック]**」タブを選択します。
1. 「**[!UICONTROL ポイント / ルール / 説明]**」セクションに移動して、このリスクの原因を表示します。

   ![](assets/s_tn_del_msg_spamassassin_ko.png)

>[!NOTE]
>
>「**[!UICONTROL スパム対策チェック]**」をクリックするたびに、SpamAssassin サービスが呼び出され、スパム対策検出のためにメッセージが再分析されます。 コンテンツを変更してから、スパム対策分析を再実行するようにしてください。
