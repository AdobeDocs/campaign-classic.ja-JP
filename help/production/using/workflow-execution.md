---
product: campaign
title: ワークフローの実行
description: ワークフローの実行
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: b5aa5663-1902-4f50-9202-783e73a28838
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 13%

---

# ワークフローの実行{#workflow-execution}



以下の節では、ワークフローの実行に関する一般的な問題と、それらのトラブルシューティング方法に関する情報を示します。

ワークフローについて詳しくは、次の節を参照してください。

* [ワークフローについて](../../workflow/using/about-workflows.md)
* [ワークフローの開始](../../workflow/using/starting-a-workflow.md)
* [ワークフローのライフサイクル](../../workflow/using/workflow-life-cycle.md)
* [ワークフローを使用する際のベストプラクティス](../../workflow/using/workflow-best-practices.md)

## キャンペーンでできるだけ早く開始 {#start-as-soon-as-possible-in-campaigns}

場合によっては、キャンペーンから実行されたワークフローが、 **[!UICONTROL 開始]** 」ボタンをクリックします。 開始する代わりに、「可能な限り早く開始」状態になります。

この問題には、いくつかの原因が考えられます。解決するには、以下の手順に従います。

1. 次を確認します。 [**[!UICONTROL operationMgt]**](../../workflow/using/about-technical-workflows.md) テクニカルワークフローのステータス。 このワークフローは、キャンペーン内のジョブまたはワークフローを管理します。 失敗した場合、ワークフローは開始/停止しません。 ワークフローを再起動して、キャンペーンワークフローの実行を再開します。

   テクニカルワークフローの監視について詳しくは、 [このページ](../../workflow/using/monitoring-technical-workflows.md).

   >[!NOTE]
   >
   >ワークフローを再開したら、保留中のタスクを必ず実行します ( **[!UICONTROL スケジューラ]** アクティビティ/ **[!UICONTROL 保留中のタスクを今すぐ実行]**) を使用して、いずれかのアクティビティで再度失敗したかどうかを確認する必要があります。

   それでもワークフローが失敗する場合は、監査ログで特定のエラーを確認し、それに応じてトラブルシューティングしてから、ワークフローを再起動します。

1. 次を確認します。 **[!UICONTROL wfserver]** モジュールの状態 **[!UICONTROL 監視]** タブ、Campaign Classicのホームページからアクセス可能 ( [プロセスの監視](../../production/using/monitoring-processes.md)) をクリックします。 このプロセスは、すべてのワークフローの実行を担当します。

   また、管理者ユーザーは、 **wfserver@`<instance>`** モジュールは、以下のコマンドを使用してメインアプリケーションサーバーで起動します。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Version X.Y (build XXXX) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをおこなっている場合、管理者ユーザーは次のコマンドを使用してサービスを再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法について詳しくは、 [この節](../../production/using/usual-commands.md#module-launch-commands).

1. をチェックします。 **実行中のキャンペーンプロセスの数** インスタンスがしきい値を超えています。 制限は [**[!UICONTROL NmsOperation_LimitConcurrency]**](../../installation/using/configuring-campaign-options.md#campaign-e-workflow-management) オプションを使用します。 この制限に達した場合、実行中のワークフローの数が上限を超える限り、ワークフローは「可能な限り早く開始」状態のままになります。

   この問題を解決するには、不要なワークフローを停止し、失敗した配信を削除します。 しきい値に達した場合は、新しいプロセスを実行できます。

   インスタンスで実行中のワークフローの数を確認するには、事前定義済みのビューを使用することをお勧めします。事前定義済みのビューは、デフォルトで **[!UICONTROL 管理]** / **[!UICONTROL 監査]** フォルダー。 詳しくは、[このページ](../../workflow/using/monitoring-workflow-execution.md#filtering-workflows-status)を参照してください。

   >[!IMPORTANT]
   >
   >を増やす **[!UICONTROL NmsOperation_LimitConcurrency]** オプションしきい値を使用すると、インスタンスのパフォーマンスに問題が生じる場合があります。 いずれの場合も、これを単独で実行しないで、Adobe Campaignの担当者にお問い合わせください。

ワークフローの監視方法について詳しくは、[この節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

## 開始中 {#start-in-progress}

ワークフローが実行されておらず、ステータスが「 **開始中**&#x200B;の場合は、ワークフローモジュールが起動されていない可能性があります。

これを確認してモジュールを開始する（必要な場合）には、次の手順を実行します。

1. 次を確認します。 **[!UICONTROL wfserver]** モジュールの状態 **[!UICONTROL 監視]** タブ、Campaign Classicのホームページからアクセス可能 ( [プロセスの監視](../../production/using/monitoring-processes.md)) をクリックします。

   また、管理者ユーザーは、 **wfserver@`<instance>`** モジュールは、以下のコマンドを使用してメインアプリケーションサーバーで起動します。

   ```
   nlserver pdump
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   [...]
   wfserver@<INSTANCENAME> (9340) - 11.3 Mb
   [...]
   ```

   モジュールの監視方法について詳しくは、 [この節](../../production/using/usual-commands.md#monitoring-commands-).

1. モジュールが実行されていない場合は、Adobeカスタマーケアにお問い合わせください。 オンプレミスインストールをおこなっている場合、管理者は次のコマンドを使用して再起動する必要があります。

   ```
   nlserver start wfserver@<INSTANCENAME>
   ```

   >[!NOTE]
   >
   >**`<instancename>`** をインスタンスの名前（production、development など）に置き換えます。インスタンス名は設定ファイルで識別されます。
   >`[path of application]nl6/conf/config-<instancename>.xml`

   モジュールの再起動方法について詳しくは、 [この節](../../production/using/usual-commands.md#module-launch-commands).

## 失敗したワークフロー {#failed-workflow}

ワークフローが失敗した場合は、次の手順に従います。

1. ワークフロージャーナルを確認します。 詳しくは、 [監視ワークフローの実行](../../workflow/using/monitoring-workflow-execution.md) および [ログを表示](../../workflow/using/monitoring-workflow-execution.md#displaying-logs) セクション。
1. テクニカルワークフローの監視. 詳しくは、 [この節](../../workflow/using/monitoring-technical-workflows.md).
1. 個々のワークフローアクティビティでエラーが発生した場合を探します。
