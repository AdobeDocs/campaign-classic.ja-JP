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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 13%

---


# ワークフローの実行{#workflow-execution}

以下の節では、ワークフローの実行に関する一般的な問題と、そのトラブルシューティング方法について説明します。

ワークフローの詳細については、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの開始](../../workflow/using/starting-a-workflow.md)
* [ワークフローのライフサイクル](../../workflow/using/workflow-life-cycle.md)
* [ワークフロー使用時のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーンで可能な限り早く開始 {#start-as-soon-as-possible-in-campaigns}

キャンペーンから実行されたワークフローが **[!UICONTROL 開始]** ボタンをクリックしたときに開始しない場合があります。 開始する代わりに、「できるだけ早く開始」状態になります。

この問題には、いくつかの原因が考えられます。次の手順に従って解決します。

1. operationMgt [****](../../workflow/using/campaign.md) 技術的なワークフローのステータスを確認します。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローは開始/停止しません。 キャンペーンワークフローの実行を再開するには、再起動します。

   テクニカルワークフローの監視の詳細については、 [このページを参照してください](../../workflow/using/monitoring-technical-workflows.md)。

   >[!NOTE]
   >
   >ワークフローを再起動したら、保留中のタスクを必ず実行し( **[!UICONTROL スケジューラー]** アクティビティを右クリックし、「保留中のタスクを **[!UICONTROL 実行」をクリックします]**)、いずれかのアクティビティで再び失敗したかどうかを確認します。

   ワークフローに失敗する場合は、監査ログで特定のエラーを確認し、それに応じてトラブルシューティングを行ってから、ワークフローを再起動します。

1. Campaign Classicのホームページからアクセスできる「 **[!UICONTROL 監視]** 」タブで、 **[!UICONTROL wfserver]** moduleの状態を確認します( [監視プロセスを参照](../../production/using/monitoring-processes.md))。 このプロセスは、すべてのワークフローの実行を担当します。

   管理者ユーザーは、次のコマンドを使用して、 **wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されているかどうかを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールを使用する場合、管理者ユーザーは次のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。 
   >`[path of application]nl6/conf/config-<instancename>.xml`

   For more on how to restart modules, refer to [this section](../../production/using/usual-commands.md#module-launch-commands).

1. インスタンスで実行中の **キャンペーンプロセスの** 数がしきい値を超えているかどうかを確認します。 NmsOperation_LimitConcurrency [****](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) オプションで定義されている制限は、インスタンス上で並行して実行できるキャンペーンプロセスの数に対して設定されています。 この上限に達すると、実行中のワークフロー数が上限を超える限り、ワークフローは「できるだけ早く開始」の状態になります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達すると、新しいプロセスの実行が許可されます。

   インスタンスの実行中のワークフロー数を確認するには、あらかじめ定義された表示を使用することをお勧めします。このは、デフォルトでは **[!UICONTROL Administration]****[!UICONTROL /]** Auditフォルダーからアクセスできます。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!CAUTION]
   >
   >NmsOperation_LimitConcurrency **** Optionのしきい値を増やすと、インスタンスのパフォーマンスの問題を引き起こす可能性があります。 いずれにしても、これを自分で実行してAdobe Campaignの連絡先に連絡することは避けてください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 開始中 {#start-in-progress}

ワークフローが実行されていない場合で、そのステータスが **開始中である場合**、ワークフローモジュールが起動していない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. Campaign Classicのホームページからアクセスできる「 **[!UICONTROL 監視]** 」タブで、 **[!UICONTROL wfserver]** moduleの状態を確認します( [監視プロセスを参照](../../production/using/monitoring-processes.md))。

   管理者ユーザーは、次のコマンドを使用して、 **wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されているかどうかを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   For more on how to monitor modules, refer to [this section](../../production/using/usual-commands.md#monitoring-commands-).

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをお持ちの場合は、次のコマンドを使用して管理者が再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。 
   >`[path of application]nl6/conf/config-<instancename>.xml`

   For more on how to restart modules, refer to [this section](../../production/using/usual-commands.md#module-launch-commands).

## 失敗したワークフロー {#failed-workflow}

ワークフローに失敗した場合は、次の手順を実行します。

1. ワークフロージャーナルを確認します。 詳細については、「 [監視ワークフローの実行](../../workflow/using/monitoring-workflow-execution.md) 」および「 [表示ログ](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) 」の項を参照してください。
1. テクニカルワークフローの監視 For more on this refer to the [this section](../../workflow/using/monitoring-technical-workflows.md).
1. 個々のワークフローアクティビティでエラーが発生した場合に検索します。
