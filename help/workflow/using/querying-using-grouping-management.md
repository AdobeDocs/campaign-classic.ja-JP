---
product: campaign
title: グループ管理を使用したクエリ
description: グループ管理を使用したクエリの実行方法を学ぶ
feature: Query Editor, Workflows
hide: true
exl-id: 23bccb48-60ab-46c9-be26-2fa35243d61e
TQID: 'https://experienceleague.adobe.com/jQoIc-ceJgiBqFrlPgDR1nm7PpcqLJedI36hnBQHrl0'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: f5293531-9312-4099-bfa3-9e67df6a8750
    internal-label: Query Editor
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 100%
---
# グループ管理を使用したクエリ {#querying-using-grouping-management}



この例では、クエリを実行して、以前の配信でターゲットとされた回数が 30 回を超えるすべてのメールドメインを検索します。

* どのテーブルを選択する必要がありますか。

  受信者テーブル (nms:recipient)

* 出力列に選択するフィールドは何ですか。

  「メールドメイン」と「プライマリキー」（カウントあり）

* データをグループ化する基準は何ですか。

  プライマリキーのカウントが 30 を超えるメールドメインを基準にします。 この操作は、「**[!UICONTROL Group by + Having]**」オプションで実行されます。 「**[!UICONTROL Group by + Having]**」では、データをグループ化し（「group by」）、グループ化した対象を選択（「having」）できます。

この例を作成するには、次の手順に従います。

1. **[!UICONTROL 汎用クエリエディター]**&#x200B;を開き、受信者テーブル（**nms:recipient**）を選択します。

   ![](assets/query_editor_02.png)

1. **[!UICONTROL 抽出するデータ]**&#x200B;ウィンドウで、「**[!UICONTROL メールドメイン]**」フィールドおよび「**[!UICONTROL プライマリキー]**」フィールドを選択します。 「**[!UICONTROL プライマリキー]**」フィールドでカウントを実行します。

   プライマリキーカウントについて詳しくは、[この節](../../platform/using/adobe-campaign-workspace.md#about-queries-in-campaign)を参照してください。

1. 「**[!UICONTROL グループを処理（GROUP BY + HAVING）]**」ボックスをオンにします。

   ![](assets/query_editor_nveau_29.png)

1. **[!UICONTROL 並べ替え]**&#x200B;ウィンドウで、メールドメインを降順で並べ替えます。 そのためには、「**[!UICONTROL 降順ソート]**」列で「**[!UICONTROL はい]**」をオンにします。 「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/query_editor_nveau_70.png)

1. **[!UICONTROL データのフィルター]**&#x200B;で、「**[!UICONTROL フィルター条件]**」を選択します。 **[!UICONTROL ターゲット要素]**&#x200B;ウィンドウに移動し、「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL データのグループ化]**&#x200B;ウィンドウで、「**[!UICONTROL 追加]**」をクリックして「**[!UICONTROL メールドメイン]**」を選択します。

   このデータのグループ化ウィンドウは、「**[!UICONTROL グループを処理（GROUP BY + HAVING]）」** ボックスをオンにした場合にのみ表示されます。

   ![](assets/query_editor_blocklist_04.png)

1. 結果で 30 回より多くターゲットとされたメールドメインのみが返される必要があるので、**[!UICONTROL グループ化条件]**&#x200B;ウィンドウで 30 より大きいプライマリキーカウントを指定します。

   このウィンドウは、「**[!UICONTROL グループを管理（GROUP BY + HAVING）]**」ボックスをオンにした場合に表示されます。このボックスでは、グループの結果をフィルターします（HAVING）。

   ![](assets/query_editor_blocklist_05.png)

1. **[!UICONTROL データフォーマット]**&#x200B;ウィンドウで、「**[!UICONTROL 次へ]**」をクリックします。ここでは書式設定は必要ありません。
1. データのプレビューウィンドウで、「**[!UICONTROL データのプレビューを開始]**」をクリックします。ここでは、ターゲットとされた回数が 30 回を超える 3 つの異なるメールドメインが返されます。

   ![](assets/query_editor_blocklist_06.png)
