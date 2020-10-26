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
translation-type: ht
source-git-commit: 75cbb8d697a95f4cc07768e6cf3585e4e079e171
workflow-type: ht
source-wordcount: '500'
ht-degree: 100%

---


# 新しいプラットフォームの開始 {#starting-new-platform}

新しいプラットフォームを設定する場合は、ドメインと IP アドレスの評判を維持することが不可欠です。

* E メール送信の開始は、プラットフォームに使用履歴がなく、この目的で IP の送信に使用されていない場合、評判もないので、繊細な手順になります。

* ISP は、当然ながら、E メールを送信するのに使用したことがなく、突然、大量の E メールトラフィックを送信し始める IP アドレスを疑います。実際に、スパム送信者は通常、「不明な」IP アドレス（ブロックリストに記載されていないアドレス）を使用して、検出前に可能な限り大量のメッセージを送信します。

* 本番フェーズの初期の出力では、運用速度に達することは期待できません。さらに、ISP によって送信アドレスがブロックされ、残りの開始フェーズに大きく影響することになるので、このままでメッセージを送信しようとしてはいけません。

新しいプラットフォームを立ち上げる際に従うべき主な原則を以下に示します。

* この情報がある場合、**無効なアドレスを強制隔離テーブルにインポート**します。
プラットフォームの開始は、多くの場合、アドレスのリストを初めて使用するときや、アドレスが完全修飾でない可能性があるときに発生します。無効なアドレスまたはハニーポットアドレスに送信すると、プラットフォームのレピュテーション低下の一因となります。

   * 無効なアドレスのリストがある場合は、初めて送信する前に、強制隔離テーブル（**[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／配信不能件数およびアドレス]**&#x200B;メニューより使用可能）にインポートすることが最善です。
   * 同様に、無効なアドレスを再評価する場合は、時間と共に不適切なアドレスの使用を減らすために、プラットフォームのレピュテーションが確立されたらおこない、少しずつ時間をかけて再評価することを強くお勧めします。

   詳しくは、[強制隔離を使用した配信の最適化](../../delivery/using/understanding-quarantine-management.md#optimizing-your-delivery-through-quarantines)を参照してください。
* mtachilds の数を制限して、**スループット率を制限**&#x200B;します。このような技術的な設定の調整について詳しくは、Adobe Campaign の管理者にお問い合わせください。
* スパムとしてマークされないように、**送信されるボリュームを順次増やします**。最初からデータベース全体をターゲットにせず、送信するたびにリストの少量を追加します。これにより、無効なアドレスの全体的な割合を減らしながら各ステップで量を増やすことができます。開始アップ段階を円滑に開発するために、ウェーブを使用できます。詳しくは、[複数のウェーブを使用した送信](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を参照してください。
* **定期的に送信**。ある程度までは、小さなものを定期的に送信する方が、大きなキャンペーンを散発的に送信するよりも適しています。
* **配信レポートに細心の注意を払う**。エラー指標の数が多い場合は、技術的な設定が正しく設定されていない可能性があります。詳しくは、[配信の監視](../../delivery/using/monitoring-a-delivery.md)を参照してください。

**関連トピック**：
* [IP ウォーミングによる E メールの評判の向上](https://helpx.adobe.com/jp/campaign/kb/increase-email-rep-ip-warming.html)
* [スパムトラップについて](https://helpx.adobe.com/jp/campaign/kb/spam-traps.html)