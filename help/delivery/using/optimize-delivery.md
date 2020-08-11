---
title: メッセージ配信の最適化
seo-title: メッセージ配信の最適化
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliveries-best-practices
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5e6ecd636ee0b2199808c03b2fd898a194f0c1ea
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 61%

---


# 配信の最適化 {#optimize-delivery}

配信の作成に入る前に、送信プロセスを保証し、最適化するためにいくつかの作業をおこないます。

以下の節では、Adobe Campaign を最適に設定するためのベストプラクティスと推奨手順について説明します。このベストプラクティスに従えば、後で問題が発生する可能性を最小限に抑えることができます。

## プラットフォームのパフォーマンス

いくつかの要因がサーバーのパフォーマンスに直接影響し、プラットフォームの速度が低下することがあります。

* パーソナライゼーション要素の数とタイプ：電子メールのパーソナライゼーションは、各受信者のデータベースからデータを取り出します。 パーソナライゼーション要素が多数ある場合は、配信の準備に必要なデータの量もそれだけ多くなります。この節のパーソナライズの詳細 [を表示します](../../delivery/using/about-personalization.md)

* サーバーの読み込み：marketing serverが多数の異なるタスクを同時に処理している場合、パフォーマンスが低下する可能性があります。 マーケティングサーバーでは、すべての配信の入出力データをすべて調整して、データが正しく、かつ時間どおりになっていることを確認する必要があります。

   **ヒント** — これを避けるには、最高のパフォーマンスを確保するために、チームの他のメンバーと配信のスケジュールを調整します。

* ワークフローの実行：ワークフローの監視は、プラットフォームのパフォーマンスの問題を回避するために不可欠です。 このドキュメントに示すガイドライン [に従います](../../workflow/using/workflow-best-practices.md#execution-and-performance)。

* ホスト対象のお客様は、 [キャンペーンコントロールパネルの機能を利用して](https://docs.adobe.com/content/help/ja-JP/control-panel/using/discover-control-panel/key-features.html) 、 [](https://docs.adobe.com/content/help/en/control-panel/using/performance-monitoring/about-performance-monitoring.html) パフォーマンス監視機能を使用してプラットフォームを監視できます。

## ネットワーク設定の確認 {#network-config}

大量の E メールを配信してもスパム送信者と間違えられないようにするために、サーバーの身元を隠そうとしない適切なネットワーク設定を使用する必要があります。

**ヒント**: ブランドのWebサイトに対応する透明な送信者アドレスを使用します。 例えば、旅行代理店の会社がバレンティノホテルチェーンを管理しているとします。 同社は、そのホテルチェーン用の Web サイトドメインとして valentino.com を所有しています。また、パリの Valentino ホテルの販促には paris.valentino.com サブドメインを使用しています。したがって、適切な送信者アドレスは hotel@paris.valentino.com などとなります。

## 配信品質の管理 {#deliverability-management}

バウンスメールが返ってきたり、スパムに指定されたりすることなく、E メールを受信者の受信ボックスに確実に届けるには、メッセージの配信品質の割合を向上させる必要があります。

* 配信品質とは何でしょうか。

   * 配信品質とは、受信者のサーバーが E メールを許可する能力を測定するためのファクターです。ISP（インターネットサービスプロバイダー）は、スパムとして識別した E メールを除外するか、E メール内の画像のダウンロードを禁止します。ISP は、特定のドメインから大量の E メールが送信されていると判断すると、その送信者から送られる E メールの許可数に上限を設定します。

   * E メールの配信品質を確認するときは、データ品質、メッセージとコンテンツ、送信インフラストラクチャ、レピュテーションという 4 つの主要カテゴリを中心に調べます。このトピックの詳細については、 [このセクションを参照してください](../../delivery/using/about-deliverability.md)。

* このドキュメントで詳しく説明 [する推奨を適用します](../../delivery/using/deliverability-key-points.md)。

* Adobeの担当者にお問い合わせください。

## 強制隔離の管理 {#quarantine-management}

強制隔離の管理プロセスを適切に維持することをお勧めします。

新しいプラットフォームで E メールの送信を開始するときは、まだ選定が十分でないアドレスのリストを使用することがあります。無効なアドレスやハニーポットアドレス（スパム送信者を誘き寄せるために作成されたメールボックス）に送信すると、プラットフォームのレピュテーションの低下につながります。適切な強制隔離管理プロセスは、次の目的に役立ちます。アドレスの質を維持し、インターネットアクセスプロバイダによるブロックリストを回避し、エラー率を低減し、配信とスループットを高速化します。

**ヒント**

* If you have a list of invalid addresses, Adobe recommends importing it to the quarantine table, through **[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Non deliverables and addresses]**.

* アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲティングされません。これによって配信が迅速になります。エラー率は配信の速度に大きく影響するからです。例えば、受信ボックスの容量が超過している場合や、アドレスが存在しない場合などに、E メールアドレスを強制隔離できます。[詳細情報](#identifying-quarantined-addresses-for-a-delivery)

* Adobe Campaign では、返されるエラーのタイプに応じて不正なアドレスを管理します。詳しくは、[この節](../../delivery/using/understanding-quarantine-management.md)を参照してください。


* 一部のインターネットアクセスプロバイダーは、無効なアドレスの割合が高すぎる場合、E メールを自動的にスパムとみなします。したがって、強制隔離を使用すると、これらのプロバイダーによってブロックリストに追加されるのを回避できます。

* 強制隔離管理は、誤った電話番号を配信から除外することで、SMSの送信コストを削減するのに役立ちます。

## 二重のオプトインのメカニズム {#double-opt-in}

無効なアドレスにメッセージが送信されるのを回避し、不適切な通信を規制し、送信者のレピュテーションを向上させるには、購読後の確認をおこなう二重のオプトインのメカニズムを実装することをお勧めします。これにより、受信者が意図的に購読したことを確認できます。

このメカニズムの実装の詳細については、 [この節で説明します](../../web/using/use-cases--web-forms.md)。
