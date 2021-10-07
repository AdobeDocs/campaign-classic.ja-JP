---
product: campaign
title: ワークフローの実行
description: ワークフローの実行
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: b5aa5663-1902-4f50-9202-783e73a28838
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 13%

---

# ワークフローの実行{#workflow-execution}

![](../../assets/v7-only.svg)

以下の節では、ワークフローの実行に関する一般的な問題とそのトラブルシューティング方法について説明します。

ワークフローについて詳しくは、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの開始](../../workflow/using/starting-a-workflow.md)
* [ワークフローのライフサイクル](../../workflow/using/workflow-life-cycle.md)
* [ワークフローを使用する際のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーンでできるだけ早く開始 {#start-as-soon-as-possible-in-campaigns}

場合によっては、キャンペーンから実行されるワークフローが「**[!UICONTROL 開始]**」ボタンをクリックしても開始されないことがあります。 開始する代わりに、「可能な限り早く開始」状態になります。

この問題には、いくつかの原因が考えられます。解決するには、以下の手順に従います。

1. [**[!UICONTROL operationMgt]**](../../workflow/using/about-technical-workflows.md) テクニカルワークフローのステータスを確認します。 キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローは開始/停止しません。 再起動して、キャンペーンワークフローの実行を再開します。

   テクニカルワークフローの監視について詳しくは、[ このページ ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。

   >[!NOTE]
   >
   >ワークフローを再起動したら、保留中のタスクを必ず実行します（**[!UICONTROL スケジューラー]** アクティビティ/ **[!UICONTROL 保留中のタスクを今すぐ実行]**）。

   それでもワークフローが失敗する場合は、監査ログで特定のエラーを確認し、それに応じてトラブルシューティングをおこない、ワークフローを再起動します。

1. Campaign Classicのホームページからアクセス可能な「**[!UICONTROL 監視]**」タブで、**[!UICONTROL wfserver]** モジュールの状態を確認します（[ 監視プロセス ](../../production/using/monitoring-processes.md) を参照）。 このプロセスは、すべてのワークフローの実行を担当します。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されたことを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをおこなっている場合、管理者ユーザーは以下のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法について詳しくは、[ この節 ](../../production/using/usual-commands.md#module-launch-commands) を参照してください。

1. インスタンス上で **を実行しているキャンペーンプロセスの数がしきい値を超えているかどうかを確認します。**[**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) オプションで定義される制限は、インスタンス上で同時に実行できるキャンペーンプロセスの数に対して適用されます。 この制限に達した場合、実行中のワークフローの数が制限を超えている限り、ワークフローは「可能な限り早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達すると、新しいプロセスの実行が許可されます。

   インスタンスで実行中のワークフローの数を確認するには、事前定義済みのビューを使用することをお勧めします。デフォルトでは **[!UICONTROL 管理]** / **[!UICONTROL 監査]** フォルダーでアクセスできます。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!IMPORTANT]
   >
   >**[!UICONTROL NmsOperation_LimitConcurrency]** オプションのしきい値を増やすと、インスタンスのパフォーマンスの問題が発生する可能性があります。 いずれの場合も、これを自分で実行しないで、Adobe Campaignの担当者にお問い合わせください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 開始中 {#start-in-progress}

ワークフローが実行されておらず、そのステータスが **開始中** の場合は、ワークフローモジュールが開始されていない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. Campaign Classicのホームページからアクセス可能な「**[!UICONTROL 監視]**」タブで、**[!UICONTROL wfserver]** モジュールの状態を確認します（[ 監視プロセス ](../../production/using/monitoring-processes.md) を参照）。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されたことを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、[ この節 ](../../production/using/usual-commands.md#monitoring-commands-) を参照してください。

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをおこなっている場合、管理者は以下のコマンドを使用して再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法について詳しくは、[ この節 ](../../production/using/usual-commands.md#module-launch-commands) を参照してください。

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順に従います。

1. ワークフロージャーナルを確認します。 詳しくは、[ ワークフローの実行の監視 ](../../workflow/using/monitoring-workflow-execution.md) および [ ログの表示 ](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) の節を参照してください。
1. テクニカルワークフローの監視. 詳しくは、[ この節 ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。
1. 個々のワークフローアクティビティでエラーを探します。
