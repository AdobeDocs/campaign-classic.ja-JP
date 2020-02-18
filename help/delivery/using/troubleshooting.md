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
source-git-commit: fa2b6890d3c9eaf7b4b6521b2edfb494faa4798c

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
>この2つのコネクタについて詳しくは、「Adobe Campaignでのモバ [イルアプリケーションの設定」を参照してください](../../delivery/using/configuring-the-mobile-application.md)。
