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
source-git-commit: aa192d975a08246ba684940fff3d33853d7d9345
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 93%

---


# 増分クエリ{#incremental-query}

増分クエリは、指標に基づいて定期的にターゲットを選択します。その際、過去にターゲティングされた人を除外します。

ターゲット済みの母集団は、ワークフローインスタンス別およびアクティビティ別にメモリに保存されています。例えば、同じテンプレートから開始される 2 つのワークフローは、同じログを共有しません。一方、同じワークフローインスタンスの同じ増分クエリに基づく 2 つのタスクは、同じログを共有します。

クエリは、標準クエリと同じ方法で定義されますが、実行はスケジュールされます。

**関連トピック：**

* [使用例： 増分クエリを使用した四半期別リストの更新](../../workflow/using/quarterly-list-update.md)
* [クエリの作成](../../workflow/using/query.md#creating-a-query)

>[!CAUTION]
>
>いずれかの増分クエリの実行時の結果が **0** と等しい場合、クエリのプログラムされた次回の実行まで、ワークフローは一時停止します。このため、増分クエリに続くトランザクションとアクティビティが、次回の実行前に処理されることはありません。

手順は次のとおりです。

1. 「**[!UICONTROL スケジュール設定と履歴]**」タブで、「**[!UICONTROL 実行をスケジュールする]**」オプションを選択します。一旦作成されたタスクはアクティブなままになり、クエリの実行スケジュールに指定された時間になるとトリガーされます。ただし、このオプションを無効にした場合、**一度に全部**&#x200B;のクエリがただちに実行されます。
1. 「**[!UICONTROL 変更]**」ボタンをクリックします。

   **[!UICONTROL スケジュール編集ウィザード]**&#x200B;ウィンドウで、頻度のタイプと、イベントの繰り返し、イベントの有効期間を設定します。

   ![](assets/s_user_segmentation_wizard_11.png)

1. 「**[!UICONTROL 完了]**」をクリックしてスケジュールを保存します。

   ![](assets/s_user_segmentation_wizard_valid.png)

1. 「**[!UICONTROL スケジュール設定と履歴]**」タブの下部セクションで、履歴として残す日数を選択できます。

   ![](assets/edit_request_inc.png)

   * **[!UICONTROL 履歴（日数）]**

      既にターゲット済みの受信者は、ターゲットされた日から履歴の最大日数に達する日まで、ログに履歴として保持されます。値がゼロの場合、受信者がログからパージされることはありません。

   * **[!UICONTROL 開始時に履歴を保持]**

      アクティビティが有効になったときに、ログがパージされないようにします。

   * **[!UICONTROL SQL テーブル名]**

      このパラメーターは、履歴データを保持するデフォルトの SQL テーブルをオーバーロードします。

## 出力パラメーター {#output-parameters}

* tableName
* schema
* recCount

この 3 つの値セットは、クエリのターゲットとなる母集団を識別します。**[!UICONTROL tableName]** はターゲットの識別子を記録するテーブル名、**[!UICONTROL schema]** は母集団のスキーマ（通常は nms:recipient）、**[!UICONTROL recCount]** はテーブル内の要素の数です。
