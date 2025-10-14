---
product: campaign
title: 配信の送信に関するトラブルシューティング
description: 配信の監視に関する問題のトラブルシューティング方法と配信パフォーマンスについて詳しく説明します。
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Monitoring, Deliverability, Troubleshooting
role: User
exl-id: 37b1d7fb-7ceb-4647-9aac-c8a80495c5bf
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 87%

---

# 配信の送信に関するトラブルシューティング {#delivery-troubleshooting}

この節では、配信を送信する際に発生する可能性のある一般的な問題と、そのトラブルシューティング方法についてリストします。

さらに、[このページ](delivery-performances.md)に記載されているベストプラクティスとチェックリストに従って、配信のパフォーマンスを確保してください。

**関連トピック：**

* [配信ステータス](delivery-statuses.md)
* [配信ダッシュボード](delivery-dashboard.md)
* [配信エラーについて](understanding-delivery-failures.md)

## 配信が遅い {#slow-deliveries}

「**[!UICONTROL 送信]**」ボタンをクリックした後に、配信が通常より長くかかっているように見えることがあります。これは様々な要素が原因として考えられます。

* 一部のメールプロバイダーが、ブロックリストに IP アドレスを追加している可能性があります。この場合は、broadLog を確認して[この節](about-deliverability.md)を参照してください。

* 迅速に処理するには配信が大きすぎる可能性があります。これは、JavaScript の高度なパーソナライゼーションで、または配信が 60KB を超えている場合に発生することがあります。Adobe Campaign v8[&#x200B; 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/delivery-best-practices.html?lang=ja){target="_blank"} を参照してください。  コンテンツガイドラインについて説明します。

* Adobe Campaign MTA 内でスロットルが発生している可能性があります。これは次の原因で発生します。

   * メッセージ保留中（**[!UICONTROL 割り当てに達しました]**&#x200B;というメッセージ）：Campaign に定義されている宣言的 MX ルールによって宣言された割り当てに達しました。このメッセージについて詳しくは、[このページ](deliverability-faq.md)を参照してください。MX ルールについて詳しくは、[この節](../../installation/using/email-deliverability.md#about-mx-rules)を参照してください。

   * メッセージ保留中（**[!UICONTROL 動的フロー制御]**&#x200B;メッセージ）：指定された ISP にメッセージを配信しようとしたときに Campaign MTA でエラーが発生しました。エラーが甚大になることでブロックリストに登録されることのないよう、低速になります。

* システムの問題によってサーバー間のインタラクションが妨げられることがあります。これにより、送信処理全体が低速になります。サーバーにメモリまたはリソースの問題がないことを確認します。これは、例えば、Campaign によるパーソナライゼーションデータの取得処理に影響することがあります。

## スケジュールされた配信 {#scheduled-deliveries-}

配信がスケジュールされた日に実行されない場合は、サーバーのタイムゾーンの違いが関係していることがあります。ミッドソーシングインスタンスとプロダクションインスタンスが異なるタイムゾーンにあることがあります。

例えば、ミッドソーシングインスタンスがブリスベンのタイムゾーンにあり、実稼動インスタンスがダーウィンのタイムゾーンにある場合、両方のタイムゾーンが互いに 30 分離れていると、監査ログで、配信が 11:56 で実稼動用にスケジュールされている場合、ミッド用にスケジュールされた同じ配信は 12 であり :2630 分の違いがあることがわかります。

## 失敗ステータス {#failed-status}

メール配信のステータスが&#x200B;**[!UICONTROL 失敗]**&#x200B;である場合は、パーソナライゼーションブロックの問題に関係している可能性があります。配信のパーソナライゼーションブロックは、例えば、スキーマが配信マッピングと一致しない場合にエラーを生成することがあります。

配信ログは、配信が失敗した理由を知るうえで重要です。配信ログから検出できる可能性のあるエラーを次に示します。

* 受信者のメッセージが次の「未到達」エラーで失敗する

  ```
  Error while compiling script 'content htmlContent' line X: `[table]` is not defined. JavaScript: error while evaluating script 'content htmlContent
  ```

  この問題の原因は、ほとんどの場合、アップストリームターゲティングまたは配信のターゲットマッピングで定義されていないか、マップされていないテーブルまたはフィールドを HTML 内のパーソナライゼーションが呼び出そうとしていることにあります。

  これを修正するには、ワークフローと配信コンテンツを確認し、問題のテーブルを呼び出そうとするパーソナライゼーションを特定して、そのテーブルをマップできるかどうかを判別する必要があります。その後、このテーブルへの呼び出しを HTML で削除するか、配信へのマッピングを修正すると解決できます。

* ミッドソーシングデプロイメントモデルで、次のメッセージが配信ログに表示されることがあります。

  ```
  Error during the call of method 'AppendDeliveryPart' on the mid sourcing server: 'Communication error with the server: please check this one is correctly configured. Code HTTP 408 'Service temporarily unavailable'.
  ```

  原因はパフォーマンスの問題に関連しています。これは、データをミッドソーシングサーバーに送信する前に、マーケティングインスタンスでデータの作成に時間がかかりすぎていることを意味します。

  これを解決するには、データベースをクリーンアップしてインデックスを再作成することをお勧めします。データベースのメンテナンスについて詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

  スケジュールされているアクティビティのすべてのワークフロー、および失敗ステータスのすべてのワークフローも再開する必要があります。[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/flow-control-activities/scheduler.html?lang=ja){target="_blank"} を参照してください。

* 配信が失敗した場合、次のエラーが配信ログに表示されることがあります。

  ```
  DLV-XXXX The count of message prepared (123) is greater than the number of messages to send (111). Please contact support.
  ```

  通常、このエラーは受信者へのメール内に複数の値があるパーソナライゼーションフィールドまたはブロックがあることを意味します。パーソナライゼーションブロックが使用されていて、特定の受信者の複数のレコードを取得しています。

  これを解決するには、使用しているパーソナライゼーションデータを確認し、それらのフィールドに複数のエントリを持つ受信者のターゲットをチェックします。配信アクティビティの前にターゲティングワークフローで&#x200B;**[!UICONTROL 重複排除]**&#x200B;アクティビティを使用して、一度に 1 つのパーソナライゼーションフィールドのみが使用されていることを確認することもできます。重複排除について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/deduplication.html?lang=ja){target="_blank"} を参照してください。

* 配信は、次の「未到達」エラーで失敗する場合があります。

  ```
  Inbound email bounce (rule 'Auto_replies' has matched this bounce).
  ```

  これは、配信が成功したものの、「Auto_replies」インバウンドメールに一致した受信者からの自動返信（「不在」返信など）を Adobe Campaign が受け取ったことを意味します。

  この自動返信メールは Adobe Campaign によって無視され、受信者のアドレスが強制隔離されることはありません。
