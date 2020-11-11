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
translation-type: ht
source-git-commit: fd75f7f75e8e77d7228233ea311dd922d100417c
workflow-type: ht
source-wordcount: '129'
ht-degree: 100%

---


# トラブルシューティング{#troubleshooting}

モバイルデバイスが Wi-Fi に接続されているにも関わらず通知を受信できない場合は、FCM または APNs のポートがファイアウォールによってブロックされていないか確認してみてください。

**Android**：モバイルデバイスは、ポート 5228 ～ 5230 で FCM サーバーに接続します。したがって、FCM への接続を許可するようにファイアウォールを設定する必要があります。開くポートは、5228（最も使用頻度が高い）、5229 および 5230 です。

**iOS**：

バイナリコネクタ：通知を送信するには、ポート 2195 でインバウンドおよびアウトバウンドの TCP トラフィックを許可する必要があります。プッシュサービスに接続されているデバイスは、ポート 5223 でインバウンドおよびアウトバウンドの TCP トラフィックを許可する必要があります。

HTTP/2 コネクタ：次のサーバーとの間での通信を許可する必要があります。

* api.push.apple.com：ポート 443
* api.development.push.apple.com：ポート 443

>[!NOTE]
>
>2 つのコネクタについて詳しくは、[Adobe Campaign でのモバイルアプリケーションの設定](../../delivery/using/configuring-the-mobile-application.md)を参照してください。
