---
product: campaign
title: トラブルシューティング
description: プッシュのトラブルシューティング
exl-id: 313eae5f-40db-4b1a-b013-f4adf8781763
source-git-commit: f05eefc9945c4ead89eb448b6e28c3523559e055
workflow-type: ht
source-wordcount: '99'
ht-degree: 100%

---

# トラブルシューティング{#troubleshooting}

![](../../assets/common.svg)

モバイルデバイスが Wi-Fi に接続されているにも関わらず通知を受信できない場合は、FCM または APNs のポートがファイアウォールによってブロックされていないか確認してみてください。

**Android**：モバイルデバイスは、ポート 5228 ～ 5230 で FCM サーバーに接続します。したがって、FCM への接続を許可するようにファイアウォールを設定する必要があります。開くポートは、5228（最も使用頻度が高い）、5229 および 5230 です。

**iOS**：

HTTP/2 コネクタ：次のサーバーとの間での通信を許可する必要があります。

* api.push.apple.com：ポート 443
* api.development.push.apple.com：ポート 443

>[!NOTE]
>
>2 つのコネクタについて詳しくは、[Adobe Campaign でのモバイルアプリケーションの設定](configuring-the-mobile-application.md)を参照してください。
