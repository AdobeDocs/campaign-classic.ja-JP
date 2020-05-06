---
title: Adobe Campaign Classic を使用した新しいプラットフォームの開始
description: Adobe Campaign Classic を使用して新しいプラットフォームを開始する際の配信品質の管理について説明します。
page-status-flag: never-activated
uuid: 2681042b-3018-42ae-b252-2367b56616bd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: 6a394eeb-fbe1-4712-bb13-db5d7965fb73
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: a1192bc804e752d13af869da66ba0505c077ed19
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 33%

---


# 新しいプラットフォームの開始 {#starting-new-platform}

新しいプラットフォームを設定する場合は、ドメインとIPアドレスの評判を維持することが不可欠です。

* 電子メールの送信を開始する手順は慎重に行う必要があります。なぜなら、プラットフォームは使用履歴を持たず、送信側IPがこの目的で使用されたことが一度もない場合は、評判が低いからです。

* ISP は、当然ながら、E メールを送信するのに使用したことがなく、突然、大量の E メールトラフィックを送信し始める IP アドレスを疑います。実際、スパム業者は、検出前に可能な限り多くのメッセージを送信するために、「不明な」IPアドレス(ブラックリスト登録済みがなかったアドレス)を一般的に使用します。

* 本番フェーズの初期の出力では、運用速度に達することは期待できません。さらに、ISP によって送信アドレスがブロックされ、残りの開始フェーズに大きく影響することになるので、このままでメッセージを送信しようとしてはいけません。

新しいプラットフォームを立ち上げる際に従うべき主な原則を以下に示します。

* この情報がある場合は、無効なアドレスを強制隔離テーブルに **インポートし**ます。
プラットフォームの開始は、多くの場合、アドレスのリストを初めて使用するときや、アドレスが完全修飾でない可能性があるときに発生します。無効なアドレスや新婚旅行先アドレスに送信すると、これはプラットフォームの評判を落とすことに役立ちます。

   * If you have a list of invalid addresses, it is in your best interests to import it into the quarantine table (available through the **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Non deliverables and addresses]** menu) before sending for the first times.
   * 同様に、無効なアドレスを再評価する場合は、時間と共に不適切なアドレスの使用を減らすために、プラットフォームのレピュテーションが確立されたらおこない、少しずつ時間をかけて再評価することを強くお勧めします。
   詳しくは、「強制隔離を使用した配信の [最適化](../../delivery/using/understanding-quarantine-management.md#optimizing-your-delivery-through-quarantines)」を参照してください。
* **相違値の数を制限して、スループット率を制限します** 。 このような技術的な設定の調整について詳しくは、Adobe Campaignの管理者にお問い合わせください。
* **スパムとしてマークされないように、送信されるボリュームを順次増やします** 。 データベース全体を開始からターゲットするのではなく、送信のたびにリストの一部を追加します。 これにより、各手順でボリュームを増やし、無効なアドレスの全体的な割合を減らすことができます。 開始アップ段階を円滑に開発するために、ウェーブを使用できます。 詳しくは、「複数のウェーブを使用した [送信](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)」を参照してください。
* **定期的に送信**。 ある程度は、大きなキャンペーンを散発的に送るよりも、定期的に小さな写真を送る方が良い。
* **配信レポートに細心の注意を払う**。 エラーインジケーターの数が多い場合は、技術設定が正しく設定されていないことを意味する可能性があります。 For more on this, see [Monitoring a delivery](../../delivery/using/monitoring-a-delivery.md).

**関連トピック**：
* [IPウォーミングによる電子メールの評判の向上](https://helpx.adobe.com/campaign/kb/increase-email-rep-ip-warming.html)
* [スパムトラップのすべて](https://helpx.adobe.com/campaign/kb/spam-traps.html)