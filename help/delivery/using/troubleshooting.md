---
title: トラブルシューティング
seo-title: トラブルシューティング
description: トラブルシューティング
seo-description: null
page-status-flag: never-activated
uuid: 02bd48cf-3928-4817-97b0-1e64cc8ad8ef
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
discoiquuid: b64c9729-cfe2-4d02-8c59-9e53efd34a96
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# トラブルシューティング{#troubleshooting}

モバイルデバイスが Wi-Fi に接続されているにも関わらず通知を受信できない場合は、FCM または APNS のポートがファイアウォールによってブロックされていないか確認してみてください。

**Android**:モバイルデバイスは、ポート5228 ～ 5230でFCMサーバーに接続します。 したがって、FCM への接続を許可するようにファイアウォールを設定する必要があります。開くポートは次のとおりです。5228（最も頻繁に使用される）、5229および5230。

**iOS**：

バイナリコネクタ：通知を送信するには、ポート 2195 でインバウンドおよびアウトバウンドの TCP トラフィックを許可する必要があります。プッシュサービスに接続されているデバイスは、ポート 5223 でインバウンドおよびアウトバウンドの TCP トラフィックを許可する必要があります。

HTTP/2 コネクタ：次のサーバーとの間での通信を許可する必要があります。

* api.push.apple.com：ポート 443
* api.development.push.apple.com：ポート 443

>[!NOTE]
>
>For more information on the two connectors, refer to [Connectors](../../delivery/using/setting-up-mobile-app-channel.md#connectors).
