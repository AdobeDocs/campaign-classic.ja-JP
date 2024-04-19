---
product: campaign
title: 配信監視の基本を学ぶ
description: Campaign Classic 配信監視機能の詳細情報
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Monitoring, Deliverability
role: User
exl-id: 9ce11da0-e37b-459e-8ec7-d2bddf59bdf7
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: ht
source-wordcount: '297'
ht-degree: 100%

---

# 配信監視の基本を学ぶ {#about-delivery-monitoring}

配信を送信後に監視することは、マーケティングキャンペーンを効率化し顧客に確実にリーチするための重要なステップです。

この節では、配信の送信後に監視できる情報の詳細、および配信の障害や強制隔離の管理方法について説明します。

<img src="assets/do-not-localize/icon_monitor.svg" width="60px">

**配信の監視**

配信のリストにより、作成したすべての配信を 1 か所にまとめて表示できます。

各配信に対して、専用のダッシュボードを使用できます。レポート、ミラーページ、除外、トラッキングログ、レンダリングなど、送信中に発生した問題の発生や、配信に関する様々なタイプの情報を監視できます。

* [配信リストへのアクセス](list-of-deliveries.md)
* [配信ダッシュボード](delivery-dashboard.md)

<img src="assets/do-not-localize/icon_guidelines.svg" width="60px">

**安全な配信パフォーマンス**

配信のパフォーマンスを確実に保つために、いくつかのガイドラインに従う必要があります。配信の送信時に発生する一般的な問題は、また、配信を効率的に送信する際に役立つものです。

* [配信のパフォーマンスとベストプラクティス](delivery-performances.md)
* [配信の送信に関わるトラブルシューティング](delivery-troubleshooting.md)

<img src="assets/do-not-localize/icon_failure.svg" width="60px">

**配信エラーの理解**

メッセージをプロファイルに送信できない場合、リモートサーバーは自動的にエラーメッセージを送信します。エラーメッセージは Adobe Campaign プラットフォームによってピックアップされ、そのメールアドレスまたは電話番号を評価して、強制隔離すべきかが判断されます。

[配信の障害を把握](understanding-delivery-failures.md)することは、マーケティングキャンペーンの改善に役立つ重要な手順です。

<img src="assets/do-not-localize/icon_quarantine.svg" width="60px">

**強制隔離管理の理解**

Adobe Campaign では、強制隔離されたアドレスのリストを管理します。アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲットにされなくなります。

[この節](understanding-quarantine-management.md)では、隔離されたアドレスを識別し管理する方法、および強制隔離にアドレスを送信する際の条件について詳しく説明します。
