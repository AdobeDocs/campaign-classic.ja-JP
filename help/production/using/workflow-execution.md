---
solution: Campaign Classic
product: campaign
title: ワークフローの実行
description: ワークフローの実行
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 13%

---


# ワークフローの実行{#workflow-execution}

以下の節では、ワークフローの実行に関する一般的な問題と、そのトラブルシューティング方法について説明します。

ワークフローの詳細については、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの開始](../../workflow/using/starting-a-workflow.md)
* [ワークフローのライフサイクル](../../workflow/using/workflow-life-cycle.md)
* [ワークフロー使用時のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーン{#start-as-soon-as-possible-in-campaigns}で可能な限り早く開始

キャンペーンから実行されたワークフローが&#x200B;**[!UICONTROL 開始]**&#x200B;ボタンをクリックしても開始にならない場合があります。 開始する代わりに、「できるだけ早く開始」状態になります。

この問題には、いくつかの原因が考えられます。次の手順に従って解決します。

1. [**[!UICONTROL operationMgt]**](../../workflow/using/campaign.md)テクニカルワークフローの状態を確認します。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローは開始/停止しません。 キャンペーンワークフローの実行を再開するには、再起動します。

   テクニカルワークフローの監視について詳しくは、[このページ](../../workflow/using/monitoring-technical-workflows.md)を参照してください。

   >[!NOTE]
   >
   >ワークフローを再起動したら、保留中のタスク(**[!UICONTROL スケジューラー]**&#x200B;アクティビティ/**[!UICONTROL 保留中のタスクを今すぐ実行]**)を右クリックして、いずれかのアクティビティで再び失敗したかどうかを確認します。

   ワークフローに失敗する場合は、監査ログで特定のエラーを確認し、それに応じてトラブルシューティングを行ってから、ワークフローを再起動します。

1. **[!UICONTROL Monitoring]**&#x200B;タブの&#x200B;**[!UICONTROL wfserver]**&#x200B;モジュールの状態を確認します。Campaign Classicのホームページからアクセスできます（[Monitoring processes](../../production/using/monitoring-processes.md)を参照）。 このプロセスは、すべてのワークフローの実行を担当します。

   管理者ユーザーは、次のコマンドを使用して、メインアプリケーションサーバー上で&#x200B;**wfserver@`<instance>`**&#x200B;モジュールが起動しているかどうかを確認することもできます。

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

   モジュールの再起動方法の詳細については、[このセクション](../../production/using/usual-commands.md#module-launch-commands)を参照してください。

1. インスタンスで&#x200B;**を実行している**&#x200B;キャンペーンプロセスの数がしきい値を超えているかどうかを確認します。 [**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management)オプションで、インスタンス上で並行して実行できるキャンペーンプロセスの数に制限が定義されています。 この上限に達すると、実行中のワークフロー数が上限を超える限り、ワークフローは「できるだけ早く開始」の状態になります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達すると、新しいプロセスの実行が許可されます。

   インスタンスの実行中のワークフロー数を確認するには、事前定義済みの表示を使用することをお勧めします。デフォルトでは、**[!UICONTROL 管理]** / **[!UICONTROL 監査]**&#x200B;フォルダー内にあります。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!IMPORTANT]
   >
   >**[!UICONTROL NmsOperation_LimitConcurrency]**&#x200B;オプションのしきい値を増やすと、インスタンスのパフォーマンスの問題を引き起こす可能性があります。 いずれにしても、これを自分で実行してAdobe Campaignの連絡先に連絡することは避けてください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 進行中の開始{#start-in-progress}

ワークフローが実行中でなく、そのステータスが&#x200B;**開始中**&#x200B;の場合は、ワークフローモジュールが起動していない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. **[!UICONTROL Monitoring]**&#x200B;タブの&#x200B;**[!UICONTROL wfserver]**&#x200B;モジュールの状態を確認します。Campaign Classicのホームページからアクセスできます（[Monitoring processes](../../production/using/monitoring-processes.md)を参照）。

   管理者ユーザーは、次のコマンドを使用して、メインアプリケーションサーバー上で&#x200B;**wfserver@`<instance>`**&#x200B;モジュールが起動しているかどうかを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、[このセクション](../../production/using/usual-commands.md#monitoring-commands-)を参照してください。

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをお持ちの場合は、次のコマンドを使用して管理者が再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。 
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法の詳細については、[このセクション](../../production/using/usual-commands.md#module-launch-commands)を参照してください。

## 失敗したワークフロー{#failed-workflow}

ワークフローに失敗した場合は、次の手順を実行します。

1. ワークフロージャーナルを確認します。 詳しくは、「[ワークフローの実行の監視](../../workflow/using/monitoring-workflow-execution.md)」および「[ログ](../../workflow/using/monitoring-workflow-execution.md#displaying-logs)を表示する」の節を参照してください。
1. テクニカルワークフローの監視 この点について詳しくは、[この](../../workflow/using/monitoring-technical-workflows.md)を参照してください。
1. 個々のワークフローアクティビティでエラーが発生した場合に検索します。
