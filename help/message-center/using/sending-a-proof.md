---
title: 配達確認の送信
seo-title: 配達確認の送信
description: 配達確認の送信
seo-description: null
page-status-flag: never-activated
uuid: 6446cc5c-8378-48d1-9486-bffbae83e28d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: message-templates
discoiquuid: 81090be2-3ed4-4f35-948b-e21af6e19999
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0ce6e5277c32bc18c20dca62e5b276f654d1ace5

---


# 配達確認の送信{#sending-a-proof}

作成済みのシードアドレスへ配達確認を送信することで、メッセージ配信をテストできます。

配達確認の送信は、通常の配信と同じ手順となります（詳しくは、[この節](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)を参照してください）。ただし、Message Center 内から配達確認を送信するためには、事前に次の操作をおこなってください。

* シードアドレスを少なくとも 1 つ作成し（[トランザクションメッセージ内のシードアドレスの管理](../../message-center/using/managing-seed-addresses-in-transactional-messages.md)を参照）、テストデータを割り当てます（[パーソナライゼーションデータ](../../message-center/using/personalization-data.md)を参照）。
* メッセージコンテツを作成します（[メッセージコンテンツの作成](../../message-center/using/creating-message-content.md)を参照）。

配達確認を送信するには：

1. 配信ウィンドウで、「**[!UICONTROL 配達確認を送信]**」ボタンをクリックします。
1. 配信を分析します。
1. エラーを修正し、配信を確認します。

   ![](assets/messagecenter_send_proof_001.png)

1. シードアドレスにメッセージが配信されたこと、およびそのコンテンツが設定どおりであることを確認します。

   ![](assets/messagecenter_send_proof_002.png)

配達確認は、各テンプレートの「**[!UICONTROL 監査]**」タブからアクセスできます。

![](assets/messagecenter_send_proof_003.png)

