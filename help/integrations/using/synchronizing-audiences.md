---
title: オーディエンスの同期
seo-title: オーディエンスの同期
description: オーディエンスの同期
seo-description: null
page-status-flag: never-activated
uuid: eda67bf7-8a0a-4240-8b31-de364be5d572
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: acs-connector
discoiquuid: 749a084e-69ee-46b4-b09b-cb91bb1da3cd
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# オーディエンスの同期{#synchronizing-audiences}

Campaign v7 の高度な機能を使用して、高度なリストを作成できます。このリストは（追加データを含め）、オーディエンスとして Campaign Standard とシームレスにリアルタイムで直接共有できます。Campaign Standard ユーザーはそのオーディエンスを Adobe Campaign Standard で使用できます。

Campaign Standard でレプリケートされない追加データを必要とする複雑なターゲティングは Campaign v7 を使用することでのみ実現できます。

また、単純に、Microsoft Dynamics などのコネクタを介して読み込まれた受信者のリストやデータを Campaign Standard と共有することもできます。

この使用例では、Campaign v7 での配信のターゲットの準備方法と、そのターゲットと追加データを Adobe Campaign Standard で作成および送信する配信で再利用する方法を示します。

>[!NOTE]
>
>必要なすべてのデータが既にレプリケートされている場合は、Adobe Campaign Standard での集計とコレクションをデータのエンリッチメントに使用することもできます。

## 前提条件 {#prerequisites}

これをおこなうには、以下が必要です。

* Campaign v7 データベースに格納され、Campaign Standard と同期された受信者。[プロファイルの同期](../../integrations/using/synchronizing-profiles.md)の節を参照してください。
* Campaign v7 データベースの nms:recipients に関連するテーブルに格納された購読またはトランザクションなどの追加データ。これらのデータは、Campaign v7 OOB スキーマまたはカスタムテーブルから取得されます。これらは同期されないので、デフォルトでは Campaign Standard では使用できません。
* Campaign v7 と Campaign Standard の両方でワークフローを実行するための権限。
* Campaign Standard で配信を作成および実行するための権限。

## Campaign v7 での追加データを含むターゲティングワークフローの作成 {#create-a-targeting-workflow-with-additional-data-in-campaign-v7}

Campaign Standard でレプリケートされない追加データを必要とする複雑なターゲティングは Campaign v7 を使用することでのみ実現できます。

ターゲットおよびその追加データが定義されると、Campaign Standard と共有できるリストとして保存できます。

>[!NOTE]
>
>これは一例です。要件によっては、単純に受信者のリストに対してクエリを実行したり、そのリストを ACS と共有したりするだけでそれ以上の処理は不要な場合もあります。また、他のデータ管理アクティビティを使用して最終ターゲットを準備することもできます。

最終オーディエンスおよびその追加データを取得するには

1. **[!UICONTROL プロファイルとターゲット]**／**[!UICONTROL ジョブ]**／**[!UICONTROL ターゲティングワークフロー]**&#x200B;で、新しいワークフローを作成します。
1. 「**[!UICONTROL クエリ]**」アクティビティを追加して、最終的な E メールを送信する受信者を選択します（例：18 ～ 30 歳のフランス在住のすべての受信者）。

   ![](assets/acs_connect_query1.png)

1. クエリ内で追加データを追加します。詳しくは、[データの追加](../../workflow/using/query.md#adding-data)の節を参照してください。

   この例では、受信者が 1 年間に受け取った配信数の集計を追加する方法を示します。

   「**[!UICONTROL クエリ]**」で、「**[!UICONTROL データを追加...]**」を選択します。

   ![](assets/acs_connect_query2.png)

1. 「**[!UICONTROL フィルタリングディメンションにリンクされたデータ]**」を選択して、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/acs_connect_query3.png)

1. 「**[!UICONTROL フィルタリングディメンションにリンクされたデータ]**」を選択して、**[!UICONTROL 受信者配信ログ]**&#x200B;ノードを選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/acs_connect_query4.png)

1. 「**[!UICONTROL 収集されたデータ]**」フィールドの「**[!UICONTROL 集計]**」を選択して、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/acs_connect_query5.png)

1. 過去 365 日間に作成されたログのみを考慮するフィルター条件を追加して、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/acs_connect_query6.png)

1. 出力列を定義します。ここで必要な列は、配信数を集計する列のみです。方法は次のとおりです。

   * ウィンドウの右側にある「**[!UICONTROL 追加]**」をクリックします。
   * **[!UICONTROL フィールドを選択]**&#x200B;ウィンドウから、「**[!UICONTROL 詳細選択]**」をクリックします。
   * 「**[!UICONTROL 集計]**」を選択してから、「**[!UICONTROL カウント]**」を選択します。「**[!UICONTROL ユニーク]**」オプションをオンにして、「**[!UICONTROL 次へ]**」をクリックします。
   * フィールドのリストで、**Count** 関数で使用したフィールドを選択します。「**[!UICONTROL プライマリキー]**」フィールドなど、常に入力されるフィールドを選択して、「**[!UICONTROL 完了]**」をクリックします。
   * **[!UICONTROL エイリアス]**&#x200B;列で、式を変更します。このエイリアスを使用すると、最終配信で追加された列を簡単に取得できます（例：**NBdeliveries**）。
   * 「**[!UICONTROL 完了]**」をクリックして、「**[!UICONTROL クエリ]**」アクティビティ設定を保存します。
   ![](assets/acs_connect_query7.png)

1. ワークフローを保存します。次の節では母集団を ACS と共有する方法について説明します。

## Campaign Standard とのターゲットの共有 {#share-the-target-with-campaign-standard}

定義済みのターゲット母集団を ACS と共有するには、「**[!UICONTROL リストの更新]**」アクティビティを使用します。

1. 前に作成したワークフローに「**[!UICONTROL リストの更新]**」アクティビティを追加して、更新または作成するリストを指定します。

   Campaign v7 でリストを保存するフォルダーを指定します。リストは実装時に定義されたフォルダーマッピングに依存します。Campaign Standard で共有すると、表示に影響する可能性があります。[権限の変更](../../integrations/using/acs-connector-principles-and-data-cycle.md#rights-conversion)の節を参照してください。

1. 「**[!UICONTROL ACS と共有]**」オプションがオンになっていることを確認します。デフォルトでオンになっています。

   ![](assets/acs_connect_listupdate1.png)

1. 保存して、ワークフローを実行します。

   ターゲットおよびその追加データは Campaign v7 のリストに保存され、即座に Campaign Standard でリストオーディエンスとして共有されます。ACS と共有されるのは既にレプリケートされているプロファイルのみです。

「**[!UICONTROL リストの更新]**」アクティビティでエラーが発生する場合、Campaign Standard との同期が失敗している可能性があります。問題の詳細を確認するには、**[!UICONTROL 管理]**／**[!UICONTROL ACS コネクタ]**／**[!UICONTROL プロセス]**／**[!UICONTROL 診断]**&#x200B;に移動します。このフォルダーには、「**[!UICONTROL リストの更新]**」アクティビティの実行でトリガーされる同期ワークフローが含まれています。[ACS コネクタのトラブルシューティング](../../integrations/using/troubleshooting-the-acs-connector.md)の節を参照してください。

## Campaign Standard でのデータの取得と配信での使用 {#retrieve-the-data-in-campaign-standard-and-use-it-in-a-delivery}

Campaign v7 でターゲティングワークフローが実行されると、Campaign Standard の&#x200B;**[!UICONTROL オーディエンス]**&#x200B;メニューから読み取り専用モードでリストオーディエンスを検索できます。

![](assets/acs_connect_deliveryworkflow_audience.png)

Campaign Standard で配信ワークフローを作成することで、このオーディエンスおよび配信に含まれる追加データを使用できるようになります。

1. **[!UICONTROL マーケティングアクティビティ]**&#x200B;メニューから新しいワークフローを作成します
1. 「**[!UICONTROL オーディエンスを読み込み]**」アクティビティを追加して、以前 Campaign v7 から共有したオーディエンスを選択します。

   このアクティビティは、選択したオーディエンスのデータを取得するために使用されます。また、必要に応じて、このアクティビティの「**[!UICONTROL ソースフィルター]**」タブを使用して、追加のソースフィルターを適用できます。

1. 「**[!UICONTROL E メール配信]**」アクティビティを追加して、他の[「E メール配信」アクティビティ](https://docs.adobe.com/content/help/ja-JP/campaign-standard/using/managing-processes-and-data/channel-activities/email-delivery.html)として設定します。
1. 配信コンテンツを開きます。
1. パーソナライゼーションフィールドの追加ポップアップから、**[!UICONTROL 追加データ（targetData）]**&#x200B;ノードを探します。このノードには、最初のターゲティングワークフローで計算されたオーディエンスの追加データが含まれます。これらは他のパーソナライゼーションフィールドとして使用できます。

   この例では、元のターゲティングワークフローから取得される追加データは、過去 365 日で各受信者に送信された配信数です。ターゲティングワークフローで指定された NBdeliveries エイリアスは、ここに表示されます。

   ![](assets/acs_connect_deliveryworkflow_targetdata.png)

1. 配信およびワークフローを保存します。

   これでワークフローを実行する準備が整いました。この後、配信の分析がおこなわれ、配信を送信する準備が整います。

   ![](assets/acs_connect_deliveryworkflow_ready.png)

## 配信の送信および監視 {#send-and-monitor-your-delivery}

配信およびそのコンテンツの準備が整った後は、[この節](https://docs.adobe.com/content/help/ja-JP/campaign-standard/using/managing-processes-and-data/channel-activities/email-delivery.html)で詳しく説明されている手順に従って配信を送信します。

1. 配信ワークフローを実行します。この手順では、送信する E メールを準備します。
1. 配信ダッシュボードから、配信を送信できることを手動で確認します。
1. 配信のレポートとログを監視します。

   * **Campaign Standard**：任意の配信について、配信に関する[レポート](https://docs.adobe.com/content/help/ja-JP/campaign-standard/using/reporting/about-reporting/about-dynamic-reports.html)および[ログ](https://docs.adobe.com/content/help/ja-JP/campaign-standard/using/testing-and-sending/monitoring-messages/monitoring-a-delivery.html)にアクセスします。
   * **Campaign v7 および Campaign Standard**：配信 ID、E メール配信ログ、E メールトラッキングログが、Campaign v7 に同期されます。Campaign v7 からマーケティングキャンペーンの包括的なビューを得ることができます。

      強制隔離は、Campaign v7 に自動的に同期されます。これにより、Campaign v7 で実行される次のターゲティングで、配信不能情報を考慮できます。

      Campaign Standard での強制隔離管理について詳しくは、[この節](https://docs.adobe.com/content/help/ja-JP/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html)を参照してください。

