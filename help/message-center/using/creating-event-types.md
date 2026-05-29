---
product: campaign
title: イベントタイプの作成
description: Adobe Campaign Classic で送信するトランザクションメッセージに一致するイベントタイプを作成する方法を説明します
feature: Transactional Messaging, Message Center
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: 98b7c827-f31d-46a6-a28d-40a78a4b4248
TQID: https://experienceleague.adobe.com/WfR-CUGmR3XeEQgBwd22RZPpSMF0Gja-7GewIIIxWug
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 192
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

1. 「**[!UICONTROL 追加]**」をクリックして、列挙の値を作成します。 注文の確認、パスワードの変更、注文の配送変更などがイベントタイプとして考えられます。

   ![](assets/messagecenter_eventtype_enum_001.png)

   >[!IMPORTANT]
   >
   >各イベントタイプは、**[!UICONTROL イベントタイプ]**&#x200B;の列挙の値と一致する必要があります。

1. 項目別リストの値を作成した後、作成事項を反映させるためには、一旦インスタンスからログオフし再度ログオンします。

>[!NOTE]
>
>**定義済みリストの操作**&#x200B;方法について詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/settings/enumerations){target=_blank}を参照してください。



