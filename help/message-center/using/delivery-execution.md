---
title: 配信の実行
seo-title: 配信の実行
description: 配信の実行
seo-description: null
page-status-flag: never-activated
uuid: d4f4cea7-783b-45d3-b004-297104f0a906
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: event-processing
discoiquuid: afb375de-2de3-47ad-8b37-664cc04864e8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 211556bbf023731ffeab2e90692410a852ab3555

---


# 配信の実行{#delivery-execution}

>[!NOTE]
>
>MTA は、トランザクションメッセージの処理を他のどの配信よりも優先します。

実行インスタンスは、エンリッチメントステージが完了し、イベントに配信テンプレートをリンクすると、配信を送信します。すべての配信がフォルダーにグループ化さ **[!UICONTROL Administration > Production > Message Center > Default > Deliveries]** れます。

![](assets/messagecenter_deliveries_execinstances_001.png)

デフォルトでは、配信は配信月ごとにサブフォルダーに並べ替えられます。

この並べ替えは、以下に示されるように、メッセージテンプレートのプロパティで変更することができます。

![](assets/messagecenter_deliveries_properties_001.png)

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールの場合、拡張MTAにアップグレードした場合は、配信品質、スループットおよびバウンス処理を向上させるために、すべてのトランザクションメッセージがAdobe Campaign拡張MTAと共に送信される場合があります。 すべての影響は標準のマーケティングメッセージと同じで、 [Adobe Campaign Enhanced MTAドキュメントで詳しく説明しています](https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html) 。