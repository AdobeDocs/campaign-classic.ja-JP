---
title: トランザクションメッセージ内のシードアドレスの管理
seo-title: トランザクションメッセージ内のシードアドレスの管理
description: トランザクションメッセージ内のシードアドレスの管理
seo-description: null
page-status-flag: never-activated
uuid: 51c4e79d-53bb-4d46-9c7d-e90066f5317d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: message-templates
discoiquuid: 12e7043e-e8b5-48a9-8a2f-99e2e6040c3c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# トランザクションメッセージ内のシードアドレスの管理{#managing-seed-addresses-in-transactional-messages}

シードアドレスを使用すると、E メールまたは SMS 配信の前に、メッセージのプレビューを表示したり、配達確認を送信したり、メッセージのパーソナライゼーションを検証したりすることができます。シードアドレスは配信に関連付けられ、その他の配信に利用することはできません。

## シードアドレスの作成 {#creating-a-seed-address}

1. In the transactional message template, click the **[!UICONTROL Seed addresses]** tab.

   ![](assets/messagecenter_create_seedaddr_001.png)

1. 後で容易に選択できるよう、ラベルを割り当てます。

   ![](assets/messagecenter_create_seedaddr_002.png)

1. シードアドレス（通信チャネルにより E メールまたは携帯電話）を入力します。

   ![](assets/messagecenter_create_seedaddr_003.png)

1. 外部識別子を入力します。このオプションのフィールドには、Web サイト上のすべてのアプリケーションに共通し、プロファイルを識別するのに利用できるビジネスキー（一意の識別子、名前 + E メールなど）を入力することができます。Adobe Campaing マーケティングデータベースにもこのフィールドが存在する場合、データベース内のプロファイルとイベントとを照合することができます。

   ![](assets/messagecenter_create_seedaddr_003bis.png)

1. テストデータを挿入します(パーソナライ [ゼーションデータ](../../message-center/using/personalization-data.md))。

   ![](assets/messagecenter_create_custo_001.png)

## 複数のシードアドレスの作成 {#creating-several-seed-addresses}

1. リンクをクリ **[!UICONTROL Add other seed addresses]** ックし、ボタンをクリック **[!UICONTROL Add]** します。

   ![](assets/messagecenter_create_seedaddr_004.png)

1. Follow the configuration steps for a seed address detailed in the [Creating a seed address](#creating-a-seed-address) section.
1. この手順を繰り返して、必要な数のアドレスを作成します。

   ![](assets/messagecenter_create_seedaddr_008.png)

アドレスを作成したら、プレビューとパーソナライゼーションを表示することができます。トランザクションメ [ッセージのプレビューを参照](../../message-center/using/transactional-message-preview.md)。
