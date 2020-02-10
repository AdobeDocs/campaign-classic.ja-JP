---
title: テストと送信に関するFAQ
seo-title: メッセージの検証、送信、および追跡
description: Campaign Classic FAQ
page-status-flag: never-activated
uuid: 3f719ac2-cc26-4fb0-adda-84666c8c38e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 16dbe423-018f-4666-9901-2120a8dc609a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 994ec35e37a1c26e83a8dd2ae31f6594cadd4c45

---


# メッセージの検証、送信、および追跡 {#validate-send-track}

## テストと検証 {#test-and-validate-before-sending}

メッセージを送信する前に、Adobe Campaign の中でテストおよび検証手順を実行する方法を学習します。

### What is the delivery analysis? {#what-is-the-delivery-analysis-}

配信分析は、ターゲット母集団が計算され、配信コンテンツが準備される段階です。この段階が完了すると、配信は送信できる状態になります。ログを参照して、問題がないことを確認します。

[詳しくはここをクリック](../../delivery/using/steps-validating-the-delivery.md)してください。

### Why should I create proofs? {#why-should-i-create-proofs-}

配達確認メッセージを作成して、メインターゲットへの送信前に承認グループに送信してテストすることを強くお勧めします。その後、メッセージのコンテンツと、パーソナライゼーションおよび配信のパラメーターを検証できます。

[詳しくはここをクリック](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)してください。[このビデオ](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/getting-started/managing-seed-and-proofs.html)もご覧ください。

### How to use seed addresses in Adobe Campaign? {#how-to-use-seed-addresses-in-adobe-campaign-}

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。シードアドレスをインポートするか、配信またはキャンペーン上で直接作成すると、それらの受信者がターゲットに追加されます。ダイレクトメール配信の場合、シードアドレスは抽出時に追加され、出力ドキュメントに織り込まれます。

この機能には次のメリットがあります。

* 受信者プロファイルにあるデータを使用してランダムにフィールドを置換可能：例えば、シードアドレスセクションなどの E メールアドレスを入力するだけで済みます。
* データ管理機能があるワークフローを使用する場合、配信で処理される追加のデータをシードアドレスのレベルで入力し、値を強制できます。これにより、ランダムな値による置換を回避します。

[シードアドレスについて詳しくはここをクリック](../../delivery/using/about-seed-addresses.md)してください。

### How can I set up an approval process before sending messages? {#how-can-i-set-up-an-approval-process-before-sending-messages-}

メッセージの設定にエラーが含まれていそうな箇所を見つけるために、配信の検証サイクルを設定することを強くお勧めします。必要に応じて、テスト受信者に配達確認を送信してコンテンツを承認するサイクルを実施します。この場合、変更を加えるたびに配達確認を送信して、コンテンツを承認することになります。

[詳しくはここをクリック](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)してください。

### What is a typology rule? {#what-is-a-typology-rule-}

キャンペーン間の競合を回避するために、Adobe Campaign では制限ルールを適用して、様々な組み合わせをテストできます。このテストにより、企業のコミュニケーションポリシーに準拠しつつ、顧客のニーズと期待に応える最適なメッセージを送信できます。

[詳しくはここをクリック](../../campaign/using/about-campaign-typologies.md)してください。

## メッセージの送信 {#send-your-messages}

Adobe Campaign で、様々なチャネルでメッセージを送信する方法を学習します。

### How can I send emails in waves? {#how-can-i-send-emails-in-waves-}

配信を大きな母集団に送信する前に、[ウェーブの設定](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)でメッセージを複数のバッチに分割して負荷を分散させることができます。

### Which are the key steps to create an email in Campaign? {#which-are-the-key-steps-to-create-an-email-in-campaign-}

E メール配信は、作成と検証が済むと送信できます。電子メールをすぐにメインターゲットに送信することも、配信を後日スケジュールすることもできます。必要に応じて、その前にターゲット母集団を推定することもできます。

[詳しくはここをクリック](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)してください。

### How to schedule a delivery? {#how-to-schedule-a-delivery-}

配信をスケジュールしたり、母集団に対する営業頻度を管理して過剰な営業活動をしないようするために、メッセージの配信を遅らせることができます。

[詳しくはここをクリック](../../delivery/using/steps-sending-the-delivery.md#scheduling-the-delivery-sending)してください。

### Can I add an attachment to emails? {#can-i-add-an-attachment-to-emails-}

Campaign Classic では、パーソナライズされた添付ファイルを電子メールに追加できます。

[電子メールの添付ファイルについて詳しくはここをクリックしてください](../../delivery/using/attaching-files.md)。

## メッセージのトラッキングと影響の測定 {#track-your-messages-and-measure-their-impact}

メッセージを送信した後で、Adobe Campaign でトラッキングして影響を測定する方法を学習します。

### How can I configure tracked links in an email delivery? {#how-can-i-configure-tracked-links-in-an-email-delivery-}

配信ごとに、メッセージの受信と、メッセージコンテンツに挿入されたリンクの有効化をトラッキングできます。これによって、ターゲットとした配信アクションに続く受信者の行動をトラッキングできます。

メッセージの各 URL について、トラッキングを有効化するかどうかの選択、リンクラベルの変更、（例えば、レポート用の）カテゴリによるリンクのグループ化をおこなうことができます。

Campaign Classic でのメッセージのトラッキング方法について[詳しくはここをクリック](../../delivery/using/about-message-tracking.md)してください。

### Where can I access delivery and tracking logs? {#where-can-i-access-delivery-and-tracking-logs-}

配信のトラッキング方法と受信者の動作については、[このページ](../../delivery/using/monitoring-a-delivery.md)を参照してください。

### Where can I get delivery reports? {#where-can-i-get-delivery-reports-}

Adobe Campaign には、配信を監視し、メッセージをトラッキングするための一連のレポートが用意されています。

[組み込みレポートについて詳しくは、ここをクリック](../../reporting/using/reports-on-deliveries.md#delivery-reports)してください。

### How does Adobe Campaign qualify and manage quarantine addresses? {#how-does-adobe-campaign-qualify-and-manage-quarantine-addresses-}

Adobe Campaign では、強制隔離されたアドレスのリストを管理します。アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲットにされなくなります。例えば、メールボックスの容量が超過している場合や、アドレスが存在しない場合などに、E メールアドレスを強制隔離できます。

[強制隔離管理について詳しくはここをクリック](../../delivery/using/understanding-quarantine-management.md)してください。
