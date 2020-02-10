---
title: イベントタイプの作成
seo-title: イベントタイプの作成
description: イベントタイプの作成
seo-description: null
page-status-flag: never-activated
uuid: 70c8325e-a6ef-4e47-85f9-a9fa04c2ef30
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: instance-configuration
discoiquuid: 5c0a428f-a3e7-4848-8c47-b72832ba97c2
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# イベントタイプの作成{#creating-event-types}

Adobe Campaign が処理するイベントのタイプは、コントロールインスタンスで作成する必要があります。This can be done via the **[!UICONTROL Administration > Platform > Enumerations]** folder of the tree. **[!UICONTROL eventType]** 列挙の値が、各イベントタイプに該当します。オーダー確認、パスワード変更またはオーダー配送変更などがイベントタイプとして考えられます。

![](assets/messagecenter_eventtype_enum_001.png)

項目別リストについて詳しくは、[列挙管理](../../platform/using/managing-enumerations.md)を参照してください。

項目別リストの値を作成した後、作成事項を反映させるためには、一旦インスタンスからログオフし、再度ログオンします。
