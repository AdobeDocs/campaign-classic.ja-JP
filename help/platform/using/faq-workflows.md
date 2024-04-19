---
product: campaign
title: ワークフローに関する FAQ
description: Campaign Classic に関する FAQ
feature: Troubleshooting, Workflows
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: 7d1bb3c6-d056-4212-9500-75459a0046fa
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: ht
source-wordcount: '362'
ht-degree: 100%

---

# ワークフローに関する FAQ {#workflows-faq}



Adobe Campaign のワークフローを使用して、複数のプロセスとタスクを調整する方法について説明します。

## ワークフローを作成するための重要な手順は？ {#what-are-the-key-steps-to-create-a-workflow-}

ワークフローを初めて作成する方法については[ここをクリック](../../workflow/using/building-a-workflow.md)：Campaign でワークフローを構築するための概念とベストプラクティスがわかります。

## Campaign でデータをインポートするにはどうすればよいですか？ {#how-can-i-import-data-in-campaign-}

データをインポートするためのベストプラクティスについては、[この節](../../platform/using/import-export-best-practices.md)を参照してください。

## ワークフローの実行を監視できますか？ {#can-i-monitor-workflow-execution-}

Campaign ワークフローの実行を監視する方法については、[このページ](../../workflow/using/starting-a-workflow.md)を参照してください。

## ワークフローで Campaign データを更新するにはどうすればよいですか？ {#how-can-i-update-campaign-data-with-a-workflow-}

データベースのデータに対する一括更新、結合、挿入を実行できます。

[詳しくはここをクリック](../../workflow/using/update-data.md)してください。

## データ管理機能を利用するにはどうすればよいですか？ {#how-can-i-leverage-data-management-capabilities-}

Adobe Campaign では、より効率的で柔軟なツールを提供することで、複雑なターゲティングの課題を解決するための一連のアクティビティを利用できます。データ管理アクティビティを使用すると、契約や購読、配信に対する反応などに関連する情報を使用して、連絡先とのすべての通信の一貫した管理の実装が可能になります。データ管理によって、セグメント化の操作時にデータのライフサイクルをトラッキングできます。具体例を以下に示します。

* データマートでモデル化されていないデータを含めることで、ターゲティングプロセスを簡素化し、最適化する（新規テーブルを作成：設定に応じた各ターゲティングワークフローへのローカル拡張）。
* 特にターゲットの構築フェーズで、またはデータベース管理中に、バッファ計算を保持し、伝達する。
* 外部データベースへのアクセス（オプション）：ターゲティングプロセス中に、異種データベースを処理する。

[詳しくはここをクリック](../../workflow/using/targeting-data.md#data-management)してください。データ管理ワークフローアクティビティを組み合わせながら、複雑なターゲットをデザインし、データを操作できるようになります。

## パーソナライズされたメッセージの送信を自動化できますか？ {#can-i-automate-personalized-messages-sending-}

競合の最高スコアに応じてパーソナライズされたメッセージをユーザーに送信する場合は、[このユースケース](../../workflow/using/enriching-data.md)を参照してください。

## ワークフローでオーディエンスをサブセットに分割するにはどうすればよいですか？ {#how-can-i-split-an-audience-in-subsets-with-a-workflow-}

ターゲットを複数のサブセットに分割する方法については、[この節](../../workflow/using/split.md)を参照してください。

## 外部ファイルの受信者データを更新するにはどうすればよいですか？ {#how-can-i-update-recipient-data-from-an-external-file-}

外部テキストファイルからの値を持つ Campaign テーブルの特定のフィールドを変更できます。

[方法についてはここをクリック](../../platform/using/import-operations-samples.md#example--enrich-the-values-with-those-of-an-external-file)してください。

## 新しい受信者を識別してターゲットにするにはどうすればよいですか？ {#how-can-i-identify-and-target-new-recipients-}

データベースに追加された最新の受信者を集計を使用して自動的に識別し、それらの受信者にあいさつメッセージを送信する方法については、[このユースケース](../../workflow/using/using-aggregates.md)を参照してください。
