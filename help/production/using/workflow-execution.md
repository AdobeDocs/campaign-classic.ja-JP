---
product: campaign
title: ワークフローの実行
description: ワークフローの実行
feature: Monitoring, Workflows
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: b5aa5663-1902-4f50-9202-783e73a28838
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '660'
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

キャンペーンから実行されたワークフローが、「**[!UICONTROL 開始]**」ボタンをクリックしても開始しない場合があります。 開始する代わりに、「できるだけ早く開始」状態になります。

この問題には複数の原因が考えられます。次の手順に従って解決してください。

1. [**[!UICONTROL operationMgt]**](../../workflow/using/about-technical-workflows.md) テクニカルワークフローステータスを確認します。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗すると、ワークフローが開始/停止しません。 再開して、キャンペーンワークフローの実行を再開します。

   テクニカルワークフローの監視については、[ このページ ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。

   >[!NOTE]
   >
   >ワークフローが再開したら、保留中のタスクが実行されていることを確認します（**[!UICONTROL スケジューラー]** アクティビティ/**[!UICONTROL 保留中のタスクを今すぐ実行]** を右クリック）。いずれかのアクティビティで再び失敗したかどうかを確認します。

   それでもワークフローが失敗する場合は、監査ログで特定のエラーを確認し、適切なトラブルシューティングを行ってから、ワークフローを再起動します。

1. Campaign Classicホームページからアクセスできる「**[!UICONTROL モニタリング]**」タブで **[!UICONTROL wfserver]** モジュールのステータスを確認します（[ プロセスのモニタリング ](../../production/using/monitoring-processes.md) を参照）。 このプロセスは、すべてのワークフローを実行します。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されていることを確認することもできます。

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

   モジュールの再起動方法については、[ この節 ](../../production/using/usual-commands.md#module-launch-commands) を参照してください。

1. インスタンス上で **実行中のキャンペーンプロセスの数** がしきい値を超えていないかどうかを確認します。 [**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) オプションでは、インスタンス上で並行して実行できるキャンペーンプロセスの数に制限があります。 この制限に達すると、実行しているワークフローの数が制限を超えている限り、ワークフローは「できるだけ早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達した場合、これにより新しいプロセスの実行が可能になります。

   インスタンスで実行されているワークフローの数を確認するには、事前定義済みのビューを使用することをお勧めします。このビューは、デフォルトで **[!UICONTROL 管理]**/**[!UICONTROL 監査]** フォルダーからアクセスできます。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!IMPORTANT]
   >
   >**[!UICONTROL NmsOperation_LimitConcurrency]** オプションのしきい値を増やすと、インスタンスのパフォーマンスの問題が発生する場合があります。 いずれの場合も、これを自分で実行せず、Adobe Campaignの担当者にお問い合わせください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 開始中 {#start-in-progress}

ワークフローが実行されておらず、ステータスが **開始中** の場合は、ワークフローモジュールが起動されていない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. Campaign Classicホームページからアクセスできる「**[!UICONTROL モニタリング]**」タブで **[!UICONTROL wfserver]** モジュールのステータスを確認します（[ プロセスのモニタリング ](../../production/using/monitoring-processes.md) を参照）。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されていることを確認することもできます。

   ```sql
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<instance-name> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、[ この節 ](../../production/using/usual-commands.md#monitoring-commands-) を参照してください。

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールを使用している場合は、管理者が次のコマンドを使用して再起動する必要があります。

   ```
   nlserver start wfserver@<instance-name>
   ```

   >[!NOTE]
   >
   >**`<instance-name>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instance-name>.xml`

   モジュールの再起動方法については、[ この節 ](../../production/using/usual-commands.md#module-launch-commands) を参照してください。

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順を実行します。

1. ワークフロージャーナルを確認します。 詳しくは、[ ワークフローの実行の監視 ](../../workflow/using/monitoring-workflow-execution.md) および [ ログの表示 ](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) の節を参照してください。
1. テクニカルワークフローを監視します。 詳しくは、[ この節 ](../../workflow/using/monitoring-technical-workflows.md) を参照してください。
1. 個々のワークフローアクティビティでエラーが発生していないかを確認します。
