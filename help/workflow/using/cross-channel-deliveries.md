---
product: campaign
title: クロスチャネル配信
description: クロスチャネル配信の詳細を説明します
feature: Workflows, Channels Activity
hide: true
exl-id: 3bb468e2-7bcf-456f-8d8f-1c4e608e2b25
TQID: 'https://experienceleague.adobe.com/BXn5nJkGD-NL8Rh5kYtltXfGJiWlYQqbyzcdZ1SleJA'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
  - id: bce277d1-7efa-48d8-9a1b-b588bb45ba1c
    internal-label: Channels Activity
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 100%
---
# クロスチャネル配信{#cross-channel-deliveries}



クロスチャネル配信は、キャンペーンワークフローアクティビティの「**[!UICONTROL 配信]**」タブから使用可能です。

使用可能な様々なチャネルを以下に示します。

* [メール](../../delivery/using/about-email-channel.md)
* [ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)
* [モバイル](../../delivery/using/sms-channel.md)
* [X（旧 Twitter）](../../social/using/about-social-marketing.md)
* [iOS](../../delivery/using/create-notifications-ios.md)
* [Android](../../delivery/using/create-notifications-android.md)

配信のベースとするテンプレートを選択し、そのコンテンツを定義します。

各種ターゲティングアクティビティを使用して、ワークフローの配信アップストリームのターゲットを指定できます。

以下の例では、プッシュ通知購読者にメールまたは SMS を送信してから 1 週間後にプッシュ通知を通知するワークフローを作成します。 手順は次のとおりです。

1. キャンペーンを作成します。
1. キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブで、ワークフローに&#x200B;**[!UICONTROL クエリ]**&#x200B;を追加します。
1. クエリを設定します。 例えば、ここでは、ターゲットディメンションとしてプッシュ通知を購読している受信者を選択します。

   >[!NOTE]
   >
   >プッシュ通知の場合は、**購読者のアプリケーション**&#x200B;のターゲットディメンションを使用します。

   ![](assets/cross_channel_delivery_1.png)

1. クエリにフィルター条件を追加します。 この場合、モバイル番号またはメールアドレスを持つ受信者を選択します。

   ![](assets/cross_channel_delivery_2.png)

1. ワークフローに&#x200B;**[!UICONTROL 分割]**&#x200B;アクティビティを追加して、モバイル番号を持つ受信者とメールアドレスを持つ受信者を分割します。
1. 「**[!UICONTROL 配信]**」タブで、各ターゲットに対する配信を選択します。

   ワークフローの配信アクティビティをダブルクリックして、従来の配信アシスタントと同じ方法で配信を作成します。 詳しくは、この[ページ](../../delivery/using/about-email-channel.md)を参照してください。

   ![](assets/cross_channel_delivery_3.png)

1. 受信者が一度に多くの配信を受信しないように、**[!UICONTROL 待機]**&#x200B;アクティビティを追加および設定します。
1. **[!UICONTROL 分割]**&#x200B;アクティビティを追加して、iOS または Android モバイルアプリケーションの購読者を分割します。

   各オペレーティングシステム用のサービスを選択します。 サービスの作成について詳しくは、この[ページ](../../delivery/using/configuring-the-mobile-application.md)を参照してください。

   ![](assets/cross_channel_delivery_4.png)

1. 各オペレーティングシステム用のモバイルアプリケーション配信を選択および設定します。

   ![](assets/cross_channel_delivery_5.png)
