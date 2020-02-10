---
title: ワークフローの実行
seo-title: ワークフローの実行
description: ワークフローの実行
seo-description: null
page-status-flag: never-activated
uuid: 115256f6-bdf2-4594-885c-e90d02a25b80
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 7d8828c5-5776-49ca-b4f7-a4a6aaaa9db1
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 69b562979f3b32a4d30dfed0695cf3cf6c0fd26a

---


# ワークフローの実行{#workflow-execution}

次の節では、ワークフローの実行に関連する一般的な問題と、それらのトラブルシューティング方法について説明します。

ワークフローについて詳しくは、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの実行](../../workflow/using/executing-a-workflow.md)
* [ワークフローを使用する場合のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーンでで可能な限り早く開始する {#start-as-soon-as-possible-in-campaigns}

場合によっては、キャンペーンから実行したワークフローが、ボタンのクリック時に開始しないことが **[!UICONTROL Start]** あります。 開始する代わりに、「可能な限り早く開始」状態になります。

この問題には、次の手順に従って解決する原因がいくつかあります。

1. 技術ワークフロー [**[!UICONTROL operationMgt]**](../../workflow/using/campaign.md) の状態を確認します。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローは開始/停止しません。 キャンペーンワークフローの実行を再開するには、キャンペーンワークフローを再起動します。

   技術ワークフローの監視の詳細については、このページを参 [照してくださ](../../workflow/using/monitoring-technical-workflows.md)い。

   >[メモ]
   >
   >ワークフローを再起動したら、いずれかのアクティビティで再び失敗したかどうかを確認するために、保留中のタスクを必ず実行します(アクティビティ/を右クリック **[!UICONTROL Scheduler]****[!UICONTROL Execute pending task(s) now]**)。

   ワークフローが失敗する場合は、監査ログで特定のエラーを確認し、適切にトラブルシューティングしてから、ワークフローを再起動します。

1. Campaign Classicホームペ **[!UICONTROL wfserver]** ージからアクセスできるタブで、モジ **[!UICONTROL Monitoring]** ュールの状態を確認します(監視プロセス [を参照](../../production/using/monitoring-processes.md))。 このプロセスは、すべてのワークフローを実行する必要があります。

   管理者ユーザーは、次のコマンドを使用して、 **メインアプリケーション`<instance>`**サーバーでwfserver@moduleが起動しているかどうかを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、アドビカスタマーケアにお問い合わせください。 オンプレミスインストールを使用している場合、管理者ユーザーは次のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >Replace **`<instancename>`** with the name of your instance (production, development, etc.). インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法の詳細については、この節を参照 [してください](../../production/using/usual-commands.md#module-launch-commands)。

1. インスタンスで実 **行されているキャンペーンプロセスの数が** 、しきい値を超えているかどうかを確認します。 インスタンス上で同時に実行でき [**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) るキャンペーンプロセスの数には、オプションで定義される制限があります。 この上限に達すると、実行中のワークフローの数が上限を超える限り、ワークフローは「できるだけ早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達すると、新しいプロセスの実行が許可されます。

   インスタンスの実行中のワークフローの数を確認するには、既定で/フォルダーからアクセス可能な定義済みのビューを使用するこ **[!UICONTROL Administration]** とをお勧め **[!UICONTROL Audit]** します。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[注意]
   >
   >オプションのしきい値 **[!UICONTROL NmsOperation_LimitConcurrency]** を増やすと、インスタンスのパフォーマンスの問題が発生する可能性があります。 いずれの場合も、この操作は自分で実行せず、Adobe Campaignの連絡先に連絡してください。

ワークフローの監視方法について詳しくは、この節を参照 [してください](../../workflow/using/monitoring-workflow-execution.md)。

## 開始中 {#start-in-progress}

ワークフローが実行されず、そのステータスが **「開始中」の場合**、ワークフローモジュールが起動していない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. Campaign Classicホームペ **[!UICONTROL wfserver]** ージからアクセスできるタブで、モジ **[!UICONTROL Monitoring]** ュールの状態を確認します(監視プロセス [を参照](../../production/using/monitoring-processes.md))。

   管理者ユーザーは、次のコマンドを使用して、 **メインアプリケーション`<instance>`**サーバーでwfserver@moduleが起動しているかどうかを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法の詳細については、この節を参照 [してください](../../production/using/usual-commands.md#monitoring-commands-)。

1. モジュールが実行されていない場合は、アドビカスタマーケアにお問い合わせください。 オンプレミスインストールを使用している場合は、次のコマンドを使用して管理者が再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >Replace **`<instancename>`** with the name of your instance (production, development, etc.). インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法の詳細については、この節を参照 [してください](../../production/using/usual-commands.md#module-launch-commands)。

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順を実行します。

1. ワークフロー仕訳帳を確認します。 詳細については、「監視ワークフローの実行 [」と「表示ログ](../../workflow/using/monitoring-workflow-execution.md) 」の節を [参照してください](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) 。
1. 技術的なワークフローを監視します。 For more on this refer to the [this section](../../workflow/using/monitoring-technical-workflows.md).
1. 個々のワークフローアクティビティでエラーが発生したかどうかを確認します。
