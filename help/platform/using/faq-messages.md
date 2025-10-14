---
product: campaign
title: テストと送信に関する FAQ
description: Campaign Classic に関する FAQ
feature: Troubleshooting
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 7fc24ef2-b021-440b-b1f2-8c77e2425328
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 88%

---

# メッセージの検証、送信およびトラッキング {#validate-send-track}



## テストと検証 {#test-and-validate-before-sending}

メッセージを送信する前に Adobe Campaign 内でテストおよび検証手順を実行する方法を説明します。

### 配信分析とは何ですか？  {#what-is-the-delivery-analysis-}

配信分析は、ターゲット母集団が計算され、配信コンテンツが準備される段階です。この段階が完了すると、配信は送信できる状態になります。ログを参照して、問題がないことを確認します。

詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/delivery-analysis.html){target="_blank"} を参照してください。

### なぜ配達確認の作成が必要なのですか？  {#why-should-i-create-proofs-}

配達確認メッセージを作成して、メインターゲットへの送信前に承認グループに送信してテストすることを強くお勧めします。その後、メッセージのコンテンツと、パーソナライゼーションおよび配信のパラメーターを検証できます。

詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/preview-and-proof.html){target="_blank"} を参照してください。

### Adobe Campaign でのシードアドレスの使用方法は？  {#how-to-use-seed-addresses-in-adobe-campaign-}

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。シードアドレスをインポートするか、配信またはキャンペーン上で直接作成すると、それらの受信者がターゲットに追加されます。ダイレクトメール配信の場合、シードアドレスは抽出時に追加され、出力ドキュメントに織り込まれます。

この機能には次のメリットがあります。

* 受信者プロファイルにあるデータを使用してランダムにフィールドを置換可能：例えば、シードアドレスセクションなどのメールアドレスを入力するだけで済みます。
* データ管理機能があるワークフローを使用する場合、配信で処理される追加のデータをシードアドレスのレベルで入力し、値を強制できます。これにより、ランダムな値による置換を回避します。

[シードアドレスについて詳しくはここをクリック](../../delivery/using/about-seed-addresses.md)してください。

### メッセージ送信前の承認プロセスを設定するにはどうすればよいですか？ {#how-can-i-set-up-an-approval-process-before-sending-messages-}

メッセージの設定にエラーが含まれていそうな箇所を見つけるために、配信の検証サイクルを設定することを強くお勧めします。必要に応じた頻度で、テスト受信者に配達確認を送信してコンテンツを承認するサイクルを実施します。この場合、変更を加えるたびに配達確認を送信して、コンテンツを承認することになります。

詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/preview-and-proof.html){target="_blank"} を参照してください。

### タイポロジルールとは何ですか？  {#what-is-a-typology-rule-}

キャンペーン間の競合を回避するために、Adobe Campaign では制限ルールを適用して、様々な組み合わせをテストできます。このテストにより、企業のコミュニケーションポリシーに準拠しつつ、顧客のニーズと期待に応える最適なメッセージを送信できます。

[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target="_blank"} を参照してください。

## メッセージの送信 {#send-your-messages}

Adobe Campaign を使用して様々なチャネルでメッセージを送信する方法について説明します。

### メールをウェーブで送信するにはどうすればよいですか？ {#how-can-i-send-emails-in-waves-}

配信を大きな母集団に送信する前に、メッセージを複数のバッチに分割して負荷を分散させるようにウェーブを設定することができます。 [Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/configure-and-send.html#sending-using-multiple-waves){target="_blank"} を参照してください。

### Campaign でメールを作成する主な手順は？  {#which-are-the-key-steps-to-create-an-email-in-campaign-}

メール配信は、作成と検証が済むと送信できます。メールをすぐにメインターゲットに送信することも、配信を後日スケジュールすることもできます。必要に応じて、その前にターゲット母集団を推定することもできます。

詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/preview-and-proof.html){target="_blank"} を参照してください。

### 配信のスケジュール方法は？  {#how-to-schedule-a-delivery-}

配信をスケジュールしたり、母集団に対する営業頻度を管理して過剰な営業活動をしないようするために、メッセージの配信を遅らせることができます。

詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/configure-and-send.html#schedule-delivery-sending){target="_blank"} を参照してください。

### メールに添付ファイルを追加できますか？  {#can-i-add-an-attachment-to-emails-}

Campaign Classic では、パーソナライズされた添付ファイルをメールに追加できます。

メールの添付ファイルについて詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/attaching-files.html?lang=ja){target="_blank"} を参照してください。

## メッセージのトラッキングと影響の測定 {#track-your-messages-and-measure-their-impact}

メッセージを送信した後で Adobe Campaign でメッセージをトラッキングし影響を測定する方法について説明します。

### メール配信でトラッキング対象リンクを設定するにはどうすればよいですか？ {#how-can-i-configure-tracked-links-in-an-email-delivery-}

配信ごとに、メッセージの受信と、メッセージコンテンツに挿入されたリンクの有効化をトラッキングできます。これによって、ターゲットとした配信アクションに続く受信者の行動をトラッキングできます。

メッセージの各 URL について、トラッキングを有効化するかどうかの選択、リンクラベルの変更、（例えば、レポート用の）カテゴリによるリンクのグループ化をおこなうことができます。

Campaign Classic でのメッセージのトラッキング方法について[詳しくはここをクリック](../../delivery/using/about-message-tracking.md)してください。

### 配信およびトラッキングのログはどこで参照できますか？  {#where-can-i-access-delivery-and-tracking-logs-}

配信のトラッキング方法と受信者の動作については、[このページ](../../delivery/using/delivery-dashboard.md)を参照してください。

### 配信レポートはどこで取得できますか？  {#where-can-i-get-delivery-reports-}

Adobe Campaign には、配信を監視し、メッセージをトラッキングするための一連のレポートが用意されています。

[ビルトインレポートについて詳しくは、ここをクリック](../../reporting/using/delivery-reports.md)してください。


### Adobe Campaign では強制隔離アドレスをどのように選定および管理していますか？  {#how-does-adobe-campaign-qualify-and-manage-quarantine-addresses-}

Adobe Campaign では、強制隔離されたアドレスのリストを管理します。アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲットにされなくなります。例えば、メールボックスの容量が超過している場合や、アドレスが存在しない場合などに、メールアドレスを強制隔離できます。

[強制隔離管理について詳しくはここをクリック](../../delivery/using/understanding-quarantine-management.md)してください。
