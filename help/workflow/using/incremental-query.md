---
title: 増分クエリ
seo-title: 増分クエリ
description: 増分クエリ
seo-description: null
page-status-flag: never-activated
uuid: 24d322e8-172c-4faa-8a1f-59085b390a76
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: targeting-activities
discoiquuid: 31071cd2-7d97-4a4f-a6cc-5ac5b6178be5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# 増分クエリ{#incremental-query}

増分クエリは、指標に基づいて定期的にターゲットを選択します。その際、過去にターゲティングされた人を除外します。

ターゲット済みの母集団は、ワークフローインスタンス別およびアクティビティ別にメモリに保存されています。例えば、同じテンプレートから開始される 2 つのワークフローは、同じログを共有しません。一方、同じワークフローインスタンスの同じ増分クエリに基づく 2 つのタスクは、同じログを共有します。

The query is defined in the same way as for standard queries (refer to [Creating a query](../../workflow/using/query.md#creating-a-query)), but its execution is scheduled.

>[!CAUTION]
>
>いずれかの増分クエリの実行時の結果が **0** と等しい場合、クエリのプログラムされた次回の実行まで、ワークフローは一時停止します。このため、増分クエリに続くトランザクションとアクティビティが、次回の実行前に処理されることはありません。

手順は次のとおりです。

1. タブで、オ **[!UICONTROL Scheduling & History]** プションを選択 **[!UICONTROL Schedule execution]** します。 一旦作成されたタスクはアクティブなままになり、クエリの実行スケジュールに指定された時間になるとトリガーされます。ただし、このオプションを無効にした場合、**一度に全部**&#x200B;のクエリがただちに実行されます。
1. ボタンをクリッ **[!UICONTROL Change]** クします。

   In the **[!UICONTROL Schedule editing wizard]** window, you can configure the type of frequency, event recurrence and event validity period.

   ![](assets/s_user_segmentation_wizard_11.png)

1. Click **[!UICONTROL Finish]** to save the schedule.

   ![](assets/s_user_segmentation_wizard_valid.png)

1. The lower section of the **[!UICONTROL Scheduling & History]** tab allows you to select the number of days to be taken into account in the history.

   ![](assets/edit_request_inc.png)

   * **[!UICONTROL History in days]**

      既にターゲット済みの受信者は、ターゲットされた日から履歴の最大日数に達する日まで、ログに履歴として保持されます。値がゼロの場合、受信者がログからパージされることはありません。

   * **[!UICONTROL Keep history when starting]**

      アクティビティが有効になったときに、ログがパージされないようにします。

   * **[!UICONTROL SQL table name]**

      このパラメーターは、履歴データを保持するデフォルトの SQL テーブルをオーバーロードします。

## 増分クエリの例：四半期ごとのリスト更新 {#example-of-an-incremental-query--quarterly-list-update}

次の例では、増分クエリを使用して、受信者リストを自動更新します。これらの受信者は、季節ごとのマーケティングキャンペーンの一部としてターゲットされています。

季節ごとのマーケティングキャンペーンでは、季節に合ったスポーツアクティビティを季節の初めに提案します。そのため、受信者リストは四半期ごとに更新されます。ただし、リストの受信者がこのキャンペーンのターゲット設定されるのは、9 ヶ月に 1 回のみにする必要があります。これにより、受信者の資格取得頻度の間隔が空き、年間を通じて季節ごとに異なるアクティビティが提供されます。

![](assets/incremental_query_example.png)

1. 新しいワークフローに、増分クエリとリスト更新アクティビティを追加します。
1. クエリーの作 **[!UICONTROL Incremental query]** 成で指定したアクティビティのタ [ブを設定します](../../workflow/using/query.md#creating-a-query)。
1. Select the **[!UICONTROL Scheduling & History]** tab and then specify a 270-day history. この指定により、既にターゲットされた受信者は、今後 270 日間（およそ 9 ヶ月間）はターゲットされません。

   Then click the **[!UICONTROL Change...]** button.

1. To ensure the list is updated before the start of each season, select **[!UICONTROL Monthly]**.
1. 次の画面で、「3 月」、「6 月」、「9 月」、「12 月」を選択します。毎月「20 日」を選択し、ワークフローの開始時刻を選択します。
1. 次に、クエリの有効期間を選択します。For example, if you want this activity to be permanently active, select **[!UICONTROL Permanent validity]**.

   ![](assets/incremental_query_example_2.png)

1. After approving the incremental query, configure the list update activity as explained in [List update](../../workflow/using/list-update.md).

このように設定しておくことで、次の季節が始まる直前にワークフローが自動的に開始されます。リストは更新され、オファーを受ける資格のある新しい受信者が含められます。

## 出力パラメーター {#output-parameters}

* tableName
* schema
* recCount

この 3 つの値セットは、クエリのターゲットとなる母集団を識別します。**[!UICONTROL tableName]** はターゲットの識別子を記録するテーブル名、**[!UICONTROL schema]** は母集団のスキーマ（通常は nms:recipient）、**[!UICONTROL recCount]** はテーブル内の要素の数です。
