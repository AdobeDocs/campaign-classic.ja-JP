---
product: campaign
title: ワークフローの実行
description: ワークフローの実行
feature: Monitoring, Workflows
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: b5aa5663-1902-4f50-9202-783e73a28838
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 14%

---

# ワークフローの実行{#workflow-execution}



以下の節では、ワークフローの実行に関する一般的な問題と、そのトラブルシューティング方法について説明します。

ワークフローの詳細については、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの開始](../../workflow/using/starting-a-workflow.md)
* [ワークフローのライフサイクル](../../workflow/using/workflow-life-cycle.md)
* [ワークフロー使用時のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーンはできるだけ早く開始 {#start-as-soon-as-possible-in-campaigns}

場合によっては、キャンペーンから実行されたワークフローが、 **[!UICONTROL 開始]** ボタン。 開始する代わりに、「できるだけ早く開始」状態になります。

この問題には複数の原因が考えられます。次の手順に従って解決してください。

1. を確認します [**[!UICONTROL operationMgt]**](../../workflow/using/about-technical-workflows.md) テクニカルワークフローステータス。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗すると、ワークフローが開始/停止しません。 再開して、キャンペーンワークフローの実行を再開します。

   テクニカルワークフローの監視について詳しくは、次を参照してください： [このページ](../../workflow/using/monitoring-technical-workflows.md).

   >[!NOTE]
   >
   >ワークフローが再開されたら、保留中のタスクを必ず実行します（ **[!UICONTROL スケジューラー]** アクティビティ / **[!UICONTROL 保留中のタスクを今すぐ実行]**）を選択して、いずれかのアクティビティで再び失敗したかどうかを確認します。

   それでもワークフローが失敗する場合は、監査ログで特定のエラーを確認し、適切なトラブルシューティングを行ってから、ワークフローを再起動します。

1. を確認します **[!UICONTROL wfserver]** でのモジュールの状態 **[!UICONTROL 監視]** タブ、Campaign Classicホームページからアクセス（を参照） [プロセスの監視](../../production/using/monitoring-processes.md)）に設定します。 このプロセスは、すべてのワークフローを実行します。

   管理者ユーザーは、 **wfserver@`<instance>`** モジュールは、以下のコマンドを使用してメインアプリケーションサーバーで起動されます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<instance-name> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールを使用している場合は、管理者ユーザーは次のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<instance-name>
   ```

   >[!NOTE]
   >
   >**`<instance-name>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instance-name>.xml`

   モジュールの再起動方法の詳細については、次を参照してください。 [この節](../../production/using/usual-commands.md#module-launch-commands).

1. 次の場合を確認します **実行中のキャンペーンプロセスの数** インスタンス上がしきい値を超えています。 によって定義された制限があります [**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) インスタンス上で並行して実行できる campaign プロセスの数に関するオプション。 この制限に達すると、実行しているワークフローの数が制限を超えている限り、ワークフローは「できるだけ早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達した場合、これにより新しいプロセスの実行が可能になります。

   インスタンスで実行されているワークフローの数を確認するには、事前定義済みのビュー（デフォルトでアクセス可能）を使用することをお勧めします **[!UICONTROL 管理]** / **[!UICONTROL 監査]** フォルダー。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!IMPORTANT]
   >
   >を増やす **[!UICONTROL NmsOperation_LimitConcurrency]** オプションのしきい値は、インスタンスのパフォーマンスの問題を引き起こす場合があります。 いずれの場合も、これを自分で実行せず、Adobe Campaignの担当者にお問い合わせください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 開始中 {#start-in-progress}

ワークフローが実行されておらず、ステータスがの場合 **開始中**、ワークフローモジュールが起動されていないことを意味する場合があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. を確認します **[!UICONTROL wfserver]** でのモジュールの状態 **[!UICONTROL 監視]** タブ、Campaign Classicホームページからアクセス（を参照） [プロセスの監視](../../production/using/monitoring-processes.md)）に設定します。

   管理者ユーザーは、 **wfserver@`<instance>`** モジュールは、以下のコマンドを使用してメインアプリケーションサーバーで起動されます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<instance-name> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、次を参照してください [この節](../../production/using/usual-commands.md#monitoring-commands-).

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールを使用している場合は、管理者が次のコマンドを使用して再起動する必要があります。

   ```
   nlserver start wfserver@<instance-name>
   ```

   >[!NOTE]
   >
   >**`<instance-name>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instance-name>.xml`

   モジュールの再起動方法の詳細については、次を参照してください。 [この節](../../production/using/usual-commands.md#module-launch-commands).

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順を実行します。

1. ワークフロージャーナルを確認します。 詳しくは、次を参照してください [ワークフローの実行の監視](../../workflow/using/monitoring-workflow-execution.md) および [ログを表示](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) セクション。
1. テクニカルワークフローを監視します。 詳しくは、次を参照してください [この節](../../workflow/using/monitoring-technical-workflows.md).
1. 個々のワークフローアクティビティでエラーが発生していないかを確認します。
