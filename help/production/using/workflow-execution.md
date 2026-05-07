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
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 27%

---

# ワークフローの実行{#workflow-execution}



以下の節では、ワークフローの実行に関する一般的な問題とそのトラブルシューティング方法について説明します。

ワークフローについて詳しくは、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ ワークフローを開始](https://experienceleague.adobe.com/docs/campaign/automation/workflows/executing-a-workflow/start-a-workflow.html?lang=ja){target="_blank"}。
* [ ワークフローライフサイクル ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/about-workflows.html?lang=ja){target="_blank"}。
* [ ワークフローの使用時のベストプラクティス ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/workflow-best-practices.html?lang=ja){target="_blank"}。

## キャンペーンをすぐに開始 {#start-as-soon-as-possible-in-campaigns}

キャンペーンから実行されたワークフローが、**[!UICONTROL 開始]** ボタンをクリックしても開始されない場合があります。 開始する代わりに、「できるだけ早く開始」状態になります。

この問題にはいくつかの原因が考えられます。以下の手順に従って解決してください。

1. [**[!UICONTROL operationMgt ]**](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/technical-workflows.html?lang=ja){target="_blank"}のテクニカルワークフローのステータスを確認します。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローが開始/停止されなくなります。 再起動して、キャンペーンワークフローの実行を再開します。

   テクニカルワークフロー監視について詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-technical-workflows.html?lang=ja){target="_blank"}を参照してください。

   >[!NOTE]
   >
   >ワークフローを再開したら、保留中のタスクを実行してください（**[!UICONTROL スケジューラー]** アクティビティを右クリック / **[!UICONTROL 保留中のタスクを今すぐ実行]**）。いずれかのアクティビティで再び失敗するかどうかを確認します。

   それでもワークフローが失敗する場合は、監査ログで特定のエラーを確認し、それに応じてトラブルシューティングを行い、ワークフローを再度再起動します。

1. Campaign Classic ホームページからアクセスできる&#x200B;**[!UICONTROL Monitoring]** タブの&#x200B;**[!UICONTROL wfserver]** モジュールの状態を確認します（[Monitoring processes](../../production/using/monitoring-processes.md)を参照）。 このプロセスはすべてのワークフローを実行する責任があります。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されていることを確認することもできます。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<instance-name> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、Adobe カスタマーケアにお問い合わせください。 オンプレミスインストールがある場合、管理者ユーザーは以下のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<instance-name>
   ```

   >[!NOTE]
   >
   >**`<instance-name>`** をインスタンスの名前（production、development など）に置き換えます。 インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instance-name>.xml`

   モジュールを再起動する方法について詳しくは、[この節](../../production/using/usual-commands.md#module-launch-commands)を参照してください。

1. インスタンスで実行しているキャンペーンプロセスの&#x200B;**件が、しきい値を超えているかどうかを確認します。**[**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) オプションで、インスタンスで同時に実行できるキャンペーンプロセスの数に制限があります。 この制限に達すると、実行中のワークフローの数が制限を超えている限り、ワークフローは「できるだけ早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達した場合、これにより新しいプロセスの実行が可能になります。

   インスタンスで実行されているワークフローの数を確認するには、**[!UICONTROL 管理]** / **[!UICONTROL 監査]** フォルダーでデフォルトでアクセスできる定義済みビューを使用することをお勧めします。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"}を参照してください。

   >[!IMPORTANT]
   >
   >**[!UICONTROL NmsOperation_LimitConcurrency]** オプションのしきい値を増やすと、インスタンスのパフォーマンスの問題が発生する可能性があります。 いずれにしても、ご自身で行うのではなく、Adobe Campaignの担当者にお問い合わせください。

ワークフローの監視方法について詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"}を参照してください。

## 進行中に開始 {#start-in-progress}

ワークフローが実行されておらず、そのステータスが&#x200B;**進行中の開始**&#x200B;の場合、ワークフローモジュールが起動しない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. Campaign Classic ホームページからアクセスできる&#x200B;**[!UICONTROL Monitoring]** タブの&#x200B;**[!UICONTROL wfserver]** モジュールの状態を確認します（[Monitoring processes](../../production/using/monitoring-processes.md)を参照）。

   管理者ユーザーは、次のコマンドを使用して、**wfserver@`<instance>`** モジュールがメインアプリケーションサーバーで起動されていることを確認することもできます。

   ```sql
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<instance-name> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、[この節](../../production/using/usual-commands.md#monitoring-commands-)を参照してください。

1. モジュールが実行されていない場合は、Adobe カスタマーケアにお問い合わせください。 オンプレミスインストールがある場合、管理者は以下のコマンドを使用してオンプレミスインストールを再起動する必要があります。

   ```
   nlserver start wfserver@<instance-name>
   ```

   >[!NOTE]
   >
   >**`<instance-name>`** をインスタンスの名前（production、development など）に置き換えます。 インスタンス名は設定ファイルによって識別されます。
   >`[path of application]nl6/conf/config-<instance-name>.xml`

   モジュールを再起動する方法について詳しくは、[この節](../../production/using/usual-commands.md#module-launch-commands)を参照してください。

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順を実行します。

1. ワークフロージャーナルを確認します。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"}を参照してください。
1. テクニカルワークフローを監視する。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-technical-workflows.html?lang=ja){target="_blank"}を参照してください。
1. 個々のワークフローアクティビティでエラーを探します。
