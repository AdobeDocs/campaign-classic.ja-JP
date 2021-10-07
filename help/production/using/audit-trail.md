---
product: campaign
title: 監査記録
description: 監査記録
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 8508d879-fb38-4b1f-9f55-0341bb8d0c67
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 7%

---

# 監査記録{#audit-trail}

![](../../assets/v7-only.svg)

Adobe Campaignでは、**[!UICONTROL 監査記録]** を使用して、インスタンス内でおこなわれた変更の完全な履歴にアクセスできます。

**[!UICONTROL 監査記録を使用すると、Adobe Campaign のインスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで記録できます。]**&#x200B;データの履歴にアクセスして次のような質問に回答するためのセルフサービスの手段が含まれています。ワークフローへの影響、最後にワークフローを更新したユーザー、またはインスタンスでユーザーがおこなった操作

>[!NOTE]
>
>Adobe Campaignでは、ユーザー権限、テンプレート、パーソナライゼーションまたはキャンペーンでおこなわれた変更は監査されません。\
>監査記録は、インスタンスの管理者のみが管理できます。

監査記録は、次の 3 つのコンポーネントで構成されます。

* **スキーマ監査記録**:アクティビティおよびスキーマに対する最後の変更を確認します。

   スキーマの詳細については、この [ ページ ](../../configuration/using/data-schemas.md) を参照してください。

* **ワークフローの監査記録**:ワークフローに対するアクティビティと最後の変更、および次のようなワークフローの状態を確認します。

   * 開始
   * 一時停止
   * 停止
   * 再度開始
   * クリーンアップ アクションのパージ履歴と等しい
   * アクションと等しいシミュレーションシミュレーションモードで開始
   * アクションと等しいウェイクアップ保留中のタスクを今すぐ実行
   * 無条件停止

   ワークフローの詳細については、この [ ページ ](../../workflow/using/about-workflows.md) を参照してください。

   ワークフローの監視方法について詳しくは、[ 専用の節 ](../../workflow/using/monitoring-workflow-execution.md) を参照してください。

* **オプションの監査記録**:アクティビティおよびオプションに対する最後の変更を確認します。

   オプションの詳細については、[ ページ ](../../installation/using/configuring-campaign-options.md) を参照してください。

## 監査記録へのアクセス {#accessing-audit-trail}

インスタンスの **[!UICONTROL 監査記録]** にアクセスするには：

1. インスタンスの **[!UICONTROL Explorer]** メニューにアクセスします。
1. **[!UICONTROL Administration]** メニューで、「**[!UICONTROL Audit]**」を選択します。

   ![](assets/audit_trail_1.png)

1. **[!UICONTROL 監査記録]** ウィンドウが開き、エンティティのリストが表示されます。 Adobe Campaignは、ワークフロー、オプションおよびスキーマの作成、編集および削除アクションに関する監査をおこないます。

   エンティティを 1 つ選択して、最後の変更の詳細を確認します。

   ![](assets/audit_trail_2.png)

1. 「**[!UICONTROL 監査エンティティ]**」ウィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL 型]** :ワークフロー、オプションまたはスキーマ。
   * **[!UICONTROL エンティティ]** :アクティビティの内部名。
   * **[!UICONTROL 変更者]** :このエンティティを最後に変更した人のユーザー名。
   * **[!UICONTROL アクション]** :このエンティティに対して最後に実行されたアクション（作成済み、編集済みまたは削除済み）。
   * **[!UICONTROL 変更日]** :このエンティティに対して最後に実行されたアクションの日付。

   コードブロックは、エンティティ内での変更に関する詳細情報を提供します。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、 **[!UICONTROL 監査ログ]** の保持期間は 180 日に設定されています。 保持期間の変更方法について詳しくは、[ ページ ](../../production/using/database-cleanup-workflow.md#deployment-wizard) を参照してください。

## 監査記録の有効化/無効化 {#enable-disable-audit-trail}

監査記録は、特定のアクティビティに対して簡単にアクティブ化または非アクティブ化できます。例えば、データベースの領域を節約する場合などです。

それには、次の手順に従います。

1. インスタンスの **[!UICONTROL Explorer]** メニューにアクセスします。
1. **[!UICONTROL 管理]** メニューで、**[!UICONTROL プラットフォーム]** を選択し、**[!UICONTROL オプション]** を選択します。

   ![](assets/audit_trail_4.png)

1. アクティブ化/非アクティブ化するエンティティに応じて、次のいずれかのオプションを選択します。

   * ワークフローの場合：**[!UICONTROL XtkAudit_Workflows]**
   * スキーマの場合：**[!UICONTROL XtkAudit_DataSchema]**
   * オプション：**[!UICONTROL XtkAudit_Option]**
   * すべてのエンティティ：**[!UICONTROL XtkAudit_Enable_All]**

   ![](assets/audit_trail_5.png)

1. エンティティを有効にする場合は **[!UICONTROL 値]** を 1 に、無効にする場合は 0 に変更します。

   ![](assets/audit_trail_6.png)

1. 「**[!UICONTROL 保存]**」をクリックします。
