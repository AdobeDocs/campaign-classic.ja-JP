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
translation-type: ht
source-git-commit: 631e29bd6e59b8ae46084dee3a1d470916a2032b
workflow-type: ht
source-wordcount: '138'
ht-degree: 100%

---


# 配信の実行{#delivery-execution}

>[!NOTE]
>
>MTA は、トランザクションメッセージの処理を他のどの配信よりも優先します。

実行インスタンスは、エンリッチメントステージが完了し、イベントに配信テンプレートをリンクすると、配信を送信します。すべての配信は、**[!UICONTROL 管理／プロダクション／Message Center／デフォルト／配信]**&#x200B;フォルダーにまとめられます。

![](assets/messagecenter_deliveries_execinstances_001.png)

デフォルトでは、配信は配信月ごとにサブフォルダーに並べ替えられます。

この並べ替えは、以下に示されるように、メッセージテンプレートのプロパティで変更することができます。

![](assets/messagecenter_deliveries_properties_001.png)

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールでは、Enhanced MTA にアップグレードしている場合、配信品質、スループットおよびバウンス処理を向上させるために、すべてのトランザクションメッセージも Adobe Campaign Enhanced MTA と共に送信される場合があります。すべての影響は標準のマーケティングメッセージと同じです。詳しくは、[Adobe Campaign Enhanced MTA](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html) ドキュメントを参照してください。