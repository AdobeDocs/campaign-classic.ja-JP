---
product: campaign
title: 監査記録
description: Campaign 監査記録を使用してインスタンスを監視する方法について説明します
feature: Audit Trail, Monitoring, Workflows
exl-id: 8508d879-fb38-4b1f-9f55-0341bb8d0c67
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 9%

---

# 監査記録{#audit-trail}



Adobe Campaignでは、 **[!UICONTROL 監査記録]** インスタンス内で行われた変更の完全な履歴にアクセスできます。

**[!UICONTROL 監査記録]** Adobe Campaign インスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで取得します。 これには、データの履歴を確認することにより、ワークフローで発生した事象、ワークフローの最終更新者、インスタンス内でユーザーが行った操作などを知るのに役立つセルフサービス式の方法が含まれています。

>[!NOTE]
>
>Adobe Campaignは、ユーザー権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更を監査しません。\
>監査記録は、インスタンスの管理者のみが管理できます。

監査記録は、次の 3 つのコンポーネントで構成されます。

* **スキーマ監査証跡**：アクティビティと、スキーマに最後に加えた変更を確認します。

  スキーマの詳細については、こちらを参照してください [ページ](../../configuration/using/data-schemas.md).

* **ワークフロー監査記録**：アクティビティ、ワークフローに最後に加えられた変更および次のようなワークフローの状態を確認します。

   * 開始
   * 一時停止
   * 停止
   * 再度開始
   * クリーンアップ：履歴をパージと同じ
   * アクション「シミュレーションモードで開始」と等しいシミュレーション
   * [ 保留中のタスクを今すぐ実行 ] アクションと同じウェイクアップ
   * 無条件停止

  ワークフローについて詳しくは、こちらを参照してください [ページ](../../workflow/using/about-workflows.md).

  ワークフローの監視方法について詳しくは、 [専用セクション](../../workflow/using/monitoring-workflow-execution.md).

* **オプション監査証跡**：アクティビティと、オプションに最後に加えた変更を確認します。

  オプションについて詳しくは、こちらを参照してください [ページ](../../installation/using/configuring-campaign-options.md).

## 監査記録へのアクセス {#accessing-audit-trail}

インスタンスにアクセスするには **[!UICONTROL 監査記録]** :

1. へのアクセス **[!UICONTROL エクスプローラー]** お使いのインスタンスのメニュー。
1. の下 **[!UICONTROL 管理]** メニュー、選択 **[!UICONTROL 監査]** .

   ![](assets/audit_trail_1.png)

1. この **[!UICONTROL 監査記録]** ウィンドウが開き、エンティティのリストが表示されます。 Adobe Campaignは、ワークフロー、オプションおよびスキーマの作成、編集および削除アクションを監査します。

   最後の変更の詳細を確認するには、いずれかのエンティティを選択します。

   ![](assets/audit_trail_2.png)

1. この **[!UICONTROL エンティティを監査]** ウィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL タイプ]** ：ワークフロー、オプションまたはスキーマ。
   * **[!UICONTROL Entity]** ：アクティビティの内部名。
   * **[!UICONTROL 変更者]** ：このエンティティを最後に変更したユーザー名。
   * **[!UICONTROL アクション]** ：このエンティティで最後に実行されたアクション（作成済み、編集済み、または削除済み）。
   * **[!UICONTROL 変更日]** ：このエンティティで最後に実行されたアクションの日付。

   コードブロックには、エンティティ内で正確に変更された内容に関する詳細情報が表示されます。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、保存期間は 180 日に設定されています。 **[!UICONTROL 監査ログ]** . 保持期間の変更方法の詳細については、こちらを参照してください [ページ](../../production/using/database-cleanup-workflow.md#deployment-wizard).

## 監査記録を有効/無効にする {#enable-disable-audit-trail}

例えば、データベースの容量を節約する場合など、監査記録を特定のアクティビティに対して簡単にアクティブ化または非アクティブ化できます。

それには、次の手順に従います。

1. へのアクセス **[!UICONTROL エクスプローラー]** お使いのインスタンスのメニュー。
1. の下 **[!UICONTROL 管理]** メニュー、選択 **[!UICONTROL Platform]** その後 **[!UICONTROL オプション]** .

   ![](assets/audit_trail_4.png)

1. アクティブ化/非アクティブ化するエンティティに応じて、次のいずれかのオプションを選択します。

   * ワークフロー： **[!UICONTROL XtkAudit_Workflows]**
   * スキーマ： **[!UICONTROL XtkAudit_DataSchema]**
   * オプション： **[!UICONTROL XtkAudit_Option]**
   * エンティティごとに、次の操作を行います。 **[!UICONTROL XtkAudit_Enable_All]**

   ![](assets/audit_trail_5.png)

1. 変更： **[!UICONTROL 値]** エンティティを有効にする場合は 1 に、無効にする場合は 0 に設定します。

   ![](assets/audit_trail_6.png)

1. クリック **[!UICONTROL 保存]** .
