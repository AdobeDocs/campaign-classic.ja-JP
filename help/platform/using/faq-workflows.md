---
title: ワークフローFAQ
seo-title: ワークフローによるプロセスの自動化とデータの管理
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
source-git-commit: 2ee1912e0de2841867d0ffb5420cc9810aa1083e

---


# ワークフローFAQ {#workflows-faq}

Adobe Campaign のワークフローを使用して、複数のプロセスとタスクを調整する方法を学習します。

## What are the key steps to create a workflow? {#what-are-the-key-steps-to-create-a-workflow-}

[最初のワークフローの作成方法についてはここをクリック](../../workflow/using/building-a-workflow.md)：Campaign でワークフローを構築するための概念とベストプラクティスがわかります。

## How can I import data in Campaign? {#how-can-i-import-data-in-campaign-}

Campaign ワークフローによってデータをインポートするためのベストプラクティスについては、[このセクション](../../workflow/using/importing-data.md)を参照してください。

## Can I monitor workflow execution? {#can-i-monitor-workflow-execution-}

Campaign ワークフローの実行を監視する方法については、[このページ](../../workflow/using/executing-a-workflow.md)を参照してください。

## How can I update Campaign data with a workflow? {#how-can-i-update-campaign-data-with-a-workflow-}

データベースのデータに対する一括更新、結合、挿入を実行できます。

[詳しくはここをクリック](../../workflow/using/update-data.md)してください。

## How can I leverage data management capabilities? {#how-can-i-leverage-data-management-capabilities-}

Adobe Campaign では、より効率的で柔軟なツールを提供することで、複雑なターゲティングの課題を解決するための一連のアクティビティを利用できます。データ管理アクティビティを使用すると、契約や購読、配信に対する反応などに関連する情報を使用して、連絡先とのすべての通信の一貫した管理の実装が可能になります。データ管理によって、セグメント化の操作時にデータのライフサイクルをトラッキングできます。具体例を以下に示します。

* データマートでモデル化されていないデータを含めることで、ターゲティングプロセスを簡素化し、最適化する（新規テーブルを作成：設定に応じた各ターゲティングワークフローへのローカル拡張）。
* 特にターゲットの構築フェーズで、またはデータベース管理中に、バッファ計算を保持し、伝達する。
* 外部データベースへのアクセス（オプション）：ターゲティングプロセス中に、異種データベースを処理する。

[詳しくはここをクリック](../../workflow/using/targeting-data.md#data-management)してください。データ管理ワークフローアクティビティを組み合わせながら、複雑なターゲットをデザインし、データを操作できるようになります。

## Can I automate personalized messages sending? {#can-i-automate-personalized-messages-sending-}

競合の最高スコアに応じてパーソナライズされたメッセージをユーザーに送信する場合は、[この使用例](../../workflow/using/enriching-data.md)を参照してください。

## How can I split an audience in subsets with a workflow? {#how-can-i-split-an-audience-in-subsets-with-a-workflow-}

ターゲットを複数のサブセットに分割する方法については、[この節](../../workflow/using/split.md)を参照してください。

## How can I update recipient data from an external file? {#how-can-i-update-recipient-data-from-an-external-file-}

外部テキストファイルからの値を持つ Campaign テーブルの特定のフィールドを変更できます。

[方法についてはここをクリック](../../platform/using/importing-data.md#example--enrich-the-values-with-those-of-an-external-file)してください。

## How can I identify and target new recipients? {#how-can-i-identify-and-target-new-recipients-}

[この使用例](../../workflow/using/using-aggregates.md)では、データベースに追加された最新の受信者を自動的に識別し、歓迎メッセージを送信する方法を理解できます。
