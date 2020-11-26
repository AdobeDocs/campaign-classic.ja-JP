---
solution: Campaign Classic
product: campaign
title: 配信
description: デフォルトの配信ワークフローの詳細を説明します
audience: workflow
content-type: reference
topic-tags: technical-workflows
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 100%

---


# 配信{#deliveries}

以下に説明するワークフローは、デフォルトでインストールされます。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">レポート集計</span> <br /> </td> 
   <td> <span class="uicontrol">reportingAggregates</span> <br /> </td> 
   <td> レポートで使用される集計を更新します。デフォルトで、毎日午前 2 時にトリガーされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">請求</span> <br /> </td> 
   <td> <span class="uicontrol">billing</span> <br /> </td> 
   <td> システムアクティビティレポートを「請求」オペレーターにメールで送信します。デフォルトで、毎月 25 日にトリガーされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">アクティブな請求プロファイルの数</span> <br /> </td> 
   <td> <span class="uicontrol">billingActiveContactCount</span> <br /> </td> 
   <td> <p>このワークフローは、アクティブなプロファイルの数をカウントします。デフォルトで、毎晩午前 1 時にトリガーされます。</p> <p>「<strong>プロファイル</strong>」とは、エンドユーザー、見込み客またはリードを表している情報のレコード（例：nmsRecipient テーブル内のレコードや、cookie ID、顧客 ID、モバイル ID、または特定のチャネルに関連するその他の情報が含まれている外部テーブル内のレコード）のことです。請求は「アクティブ」なプロファイルのみに関係します。過去 12 ヶ月以内にいずれかのチャネルでターゲットになるか通信がおこなわれたプロファイルは「アクティブ」とみなされます。</p> <p>ただし、Facebook および Twitter チャネルは考慮されません。</p> <p><span class="uicontrol">アクティブなプロファイルの数</span>の概要は、<span class="uicontrol">管理</span>／<span class="uicontrol">キャンペーン管理</span>／<span class="uicontrol">顧客指標</span>メニューから表示できます。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">エイリアスクレンジング</span> <br /> </td> 
   <td> <span class="uicontrol">aliasCleansing</span> <br /> </td> 
   <td> 列挙値を標準化します。デフォルトで、毎日午前 3 時にトリガーされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">配信品質の更新</span> <br /> </td> 
   <td> <span class="uicontrol">deliverabilityUpdate</span> <br /> </td> 
   <td> バウンスメールの選定ルールのリストと、ドメインのリストとプラットフォームの MX のリストを作成できます。このワークフローは、HTTPS ポートが開かれている場合にのみ機能します。これらのリストは配信品質モジュールがインストールされていない場合、更新されません。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">データベースのクリーンアップ</span> <br /> </td> 
   <td> <span class="uicontrol">cleanup</span> <br /> </td> 
   <td> <p>データベースのメンテナンスワークフローです。統計とプロセスの各種の計算をおこない、デプロイメントアシスタント内の定義済みの設定に応じてデータベースから古いデータを削除します。デフォルトで、毎日午前 4 時にトリガーされます。</p> <p>詳しくは、この<a href="../../production/using/database-cleanup-workflow.md">ページ</a>を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">一時停止されたワークフローのクリーンアップ</span> <br /> </td> 
   <td> <span class="uicontrol">cleanupPausedWorkflows</span> <br /> </td> 
   <td> <p>このワークフローは、重要度が通常に設定された一時停止中のワークフローを分析し、長期間一時停止状態が続いている場合に警告と通知をトリガーします。1 ヶ月後、一時停止中のテクニカルワークフローは無条件で停止されます。デフォルトで、毎週月曜日の午前 5 時にトリガーされます。</p> <p>詳しくは、<a href="../../workflow/using/monitoring-workflow-execution.md#handling-of-paused-workflows" target="_blank">一時停止されたワークフローの処理</a>を参照してください。</p></td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">オファー通知</span> <br /> </td> 
   <td> <span class="uicontrol">offerMgt</span> <br /> </td> 
   <td> 承認されたオファーと、オファーカタログに含まれるすべてのカテゴリをオンライン環境にデプロイします。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">プレビュー</span> <br /> </td> 
   <td> <span class="uicontrol">forecasting</span> <br /> </td> 
   <td> 暫定カレンダー（暫定ログを作成）に保存された配信を分析します。デフォルトで、毎日午前 1 時にトリガーされます。<br /> </td> 
  </tr> 
  <tr> 
   <td> <span class="uicontrol">トラッキング</span> <br /> </td> 
   <td> <span class="uicontrol">tracking</span> <br /> </td> 
   <td> トラッキング情報のリカバリと紐付けを実行します。トラッキングおよび配信の統計情報、特に Message Center のアーカイブワークフローで使用される統計情報の再計算を保証します。デフォルトでは、1 時間に 1 回トリガーされます。<br /> </td> 
  </tr> 
 </tbody> 
</table>

