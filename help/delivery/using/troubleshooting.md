---
solution: Campaign Classic
product: campaign
title: トラブルシューティング
description: トラブルシューティング
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '128'
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
