---
product: campaign
title: イベントタイプの作成
description: Adobe Campaign Classic で送信するトランザクションメッセージに一致するイベントタイプを作成する方法を説明します
feature: Transactional Messaging, Message Center
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: 98b7c827-f31d-46a6-a28d-40a78a4b4248
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: ht
source-wordcount: '177'
ht-degree: 100%

---

# イベントタイプの作成 {#creating-event-types}



各イベントをパーソナライズされたメッセージに変更するには、まず&#x200B;**イベントタイプ**&#x200B;を作成します。

[メッセージテンプレートを作成](../../message-center/using/creating-the-message-template.md)する際、送信するメッセージに一致するイベントのタイプを選択します。

>[!IMPORTANT]
>
>イベントタイプをメッセージテンプレートで使用するには、事前に作成しておく必要があります。

Adobe Campaign で処理されるイベントタイプを作成するには、次の手順に従います。

1. **コントロールインスタンス**&#x200B;にログオンします。

1. ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／列挙]**&#x200B;フォルダーに移動します。

1. リストから&#x200B;**[!UICONTROL イベントタイプ]**&#x200B;を選択します。

1. 「**[!UICONTROL 追加]**」をクリックして、列挙の値を作成します。注文の確認、パスワードの変更、注文の配送変更などがイベントタイプとして考えられます。

   ![](assets/messagecenter_eventtype_enum_001.png)

   >[!IMPORTANT]
   >
   >各イベントタイプは、**[!UICONTROL イベントタイプ]**&#x200B;の列挙の値と一致する必要があります。

1. 項目別リストの値を作成した後、作成事項を反映させるためには、一旦インスタンスからログオフし再度ログオンします。

>[!NOTE]
>
>項目別リストの詳細については、[列挙の管理](../../platform/using/managing-enumerations.md)を参照してください。


