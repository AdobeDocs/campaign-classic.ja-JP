---
product: campaign
title: データのライフサイクル
description: ワークフローにおけるデータのライフサイクルの詳細について説明します
feature: Workflows, Data Management
hide: true
exl-id: 366acc1e-d769-4053-9fa1-f47182627c07
TQID: https://experienceleague.adobe.com/eRSi9Eu1u9pMtMiiMZI9kZLjZ1JAWCt5B4HFc4FAm3U
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 548
ht-degree: 100%

---

# データのライフサイクル {#data-life-cycle}



## ワークテーブル {#work-table}

ワークフローでは、1 つのアクティビティから別のアクティビティへ移されたデータは、一時的なワークテーブルに保存されます。

このデータは、適切なトランジションを右クリックすることで、表示して分析することができます。

![](assets/wf-right-click-analyze.png)

これを実行するには、該当するメニューを選択します。

* ターゲットを表示

  このメニューは、ターゲット母集団に対して使用可能なデータと、ワークテーブルの構造を表示します（「**[!UICONTROL スキーマ]**」タブ）。

  ![](assets/wf-right-click-display.png)

  詳しくは、[ワークテーブルとワークフローのスキーマ](monitoring-workflow-execution.md#worktables-and-workflow-schema)を参照してください。

* ターゲットを分析

  このメニューは、トランジションのデータの統計とレポートを作成できる記述的分析アシスタントを表示します。

  詳しくは、[この節](../../reporting/using/using-the-descriptive-analysis-wizard.md)を参照してください。

ワークフローが実行されると、ターゲットデータはパージされます。 最後のワークテーブルだけにアクセスできます。 ワークフローを設定し、すべてのワークテーブルをアクセス可能なまま維持することもできます。それには、「**[!UICONTROL 2 つの実行間の中間母集団の結果を保存]**」オプションを選択します。

ただし、データが大量にある場合、このオプションを有効化しないことをお勧めします。

![](assets/wf-purge-data-option.png)

## データのターゲット {#target-data}

ワークフローのワークテーブルに保存されたデータは、パーソナライゼーションフィールドからアクセスできます。

このようにすることで、リストを経由して収集したデータ、または調査に対する回答に基づくデータを使用できます。 それには、次の構文を使用します。

```
%= targetData.FIELD %
```

「**[!UICONTROL ターゲット式]**」（targetData）タイプのパーソナライゼーション要素は、ターゲティングワークフローには使用できません。 配信ターゲットは、ワークフロー内に作成され、配信のインバウンドトランジション内に指定される必要があります。

配信の配達確認を作成するには、パーソナライゼーションデータが入力できるように、配達確認のターゲットが&#x200B;**[!UICONTROL アドレス置換]**&#x200B;モードに基づいて作成される必要があります。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-message.html?lang=ja#target-population){target="_blank"}のこの節を参照してください。

次の例では、パーソナライズしたメールで使用するために、顧客に関する情報のリストを収集しようとしています。

次の手順に従います。

1. 情報を収集するワークフローを作成し、既にデータベース内にあるデータと紐付けをおこなってから、配信を開始します。

   ![](assets/wf-targetdata-sample-1.png)

   この例では、ファイルの内容は次のようになります。

   ```
   Music,First name,Last name,Account,CD/DVD,Card
   Pop,David,BLAIR,4323,CD,0
   Rock,Daniel,ARCARI,3222,DVD,1
   Disco,Uma,ALTON,0488,DVD,0
   Jazz,Paul,BOLES,6475,CD,1
   Jazz,David,BOUKHARI,0841,DVD,1
   [...]
   ```

   ファイルを読み込むには、次の手順を適用します。

   ![](assets/wf-targetdata-sample-2.png)

1. 「**[!UICONTROL エンリッチメント]**」タイプアクティビティを設定し、収集したデータを、既に Adobe Campaign データベース内にあるデータと紐付けします。

   ここでは、紐付けキーがアカウント番号です。

   ![](assets/wf-targetdata-sample-3.png)

1. 次に、テンプレートに基づいて作成され、インバウンドトランジションによって受信者が指定された「**[!UICONTROL 配信]**」を設定します。

   ![](assets/wf-targetdata-sample-4.png)

   >[!CAUTION]
   >
   >トランジションに含まれているデータのみが、配信のパーソナライズに使用されます。 「**targetData**」タイプのパーソナライゼーションフィールドは、「**[!UICONTROL 配信]**」アクティビティのインバウンドの母集団用にのみ使用可能です。

1. 配信テンプレートで、ワークフローで収集したフィールドを使用します。

   それには、「**[!UICONTROL ターゲット式]**」タイプのパーソナライゼーションフィールドを挿入します。

   ![](assets/wf-targetdata-sample-5.png)

   ここでは、ワークフローで収集されたファイル内に記述された顧客の好きな音楽ジャンルとメディアタイプ（CD または DVD）を挿入します。

   さらに、ロイヤルティのあるカード所有者（例えば Card の値が 1 と等しい受信者）にクーポンを追加します。

   ![](assets/wf-targetdata-sample-6.png)

   「**[!UICONTROL ターゲット式]**」（targetData）タイプのデータが、すべてのパーソナライゼーションフィールドと同じ特性を使用して、配信に挿入されます。 これらのデータは、本文、リンクラベル、またはリンク自体に使用されます。

   収集された受信者宛てのメッセージには、次のデータが含まれます。

   ![](assets/wf-targetdata-sample-7.png)
