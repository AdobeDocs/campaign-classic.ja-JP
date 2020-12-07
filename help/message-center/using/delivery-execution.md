---
solution: Campaign Classic
product: campaign
title: 配信の実行
description: 配信の実行
audience: message-center
content-type: reference
topic-tags: event-processing
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '136'
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