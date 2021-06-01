---
solution: Campaign Classic
product: campaign
title: イベントタイプの作成
description: Adobe Campaign Classicで送信するトランザクションメッセージに一致するイベントタイプを作成する方法を説明します。
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: 98b7c827-f31d-46a6-a28d-40a78a4b4248
source-git-commit: d39b15b0efc6cbd6ab24e074713be6f8fc90e5fc
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 15%

---

# イベントタイプの作成 {#creating-event-types}

各イベントをパーソナライズされたメッセージに確実に変更するには、まず&#x200B;**イベントタイプ**&#x200B;を作成する必要があります。

[メッセージテンプレート](../../message-center/using/creating-the-message-template.md)を作成する際に、送信するメッセージに一致するイベントのタイプを選択します。

>[!IMPORTANT]
>
>イベントタイプをメッセージテンプレートで使用するには、事前に作成しておく必要があります。

Adobe Campaignで処理されるイベントタイプを作成するには、次の手順に従います。

1. **コントロールインスタンス**&#x200B;にログオンします。

1. ツリーの&#x200B;**[!UICONTROL 管理/プラットフォーム/列挙]**&#x200B;フォルダーに移動します。

1. リストから&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;を選択します。

1. 「**[!UICONTROL 追加]**」をクリックして、列挙値を作成します。 注文確認、パスワード変更、注文配送の変更などが該当します。

   ![](assets/messagecenter_eventtype_enum_001.png)

   >[!IMPORTANT]
   >
   >各イベントタイプは、**[!UICONTROL イベントタイプ]**&#x200B;列挙の値と一致する必要があります。

1. 項目別リストの値を作成した後、作成事項を反映させるためには、一旦インスタンスからログオフし、再度ログオンします。

>[!NOTE]
>
>[列挙管理](../../platform/using/managing-enumerations.md)の項目別リストの詳細を説明します。


