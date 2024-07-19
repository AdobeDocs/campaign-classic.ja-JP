---
product: campaign
title: 監査記録
description: Campaign 監査記録を使用してインスタンスを監視する方法について説明します
feature: Audit Trail, Monitoring, Workflows
exl-id: 8508d879-fb38-4b1f-9f55-0341bb8d0c67
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 64%

---

# 監査記録{#audit-trail}



Adobe Campaignでは、**[!UICONTROL 監査記録]** を使用すると、インスタンス内で行われた変更の全履歴にアクセスできます。

**[!UICONTROL 監査記録]** は、Adobe Campaign インスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで記録します。 これには、データの履歴を確認することにより、ワークフローで発生した事象、ワークフローの最終更新者、インスタンス内でユーザーが行った操作などを知るのに役立つセルフサービス式の方法が含まれています。

>[!NOTE]
>
>Adobe Campaign では、ユーザー権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更を監査しません。\
>監査記録は、インスタンスの管理者のみが管理できます。

監査記録は、次の 3 つのコンポーネントで構成されます。

* **スキーマ監査証跡**: アクティビティと、スキーマに最後に加えられた変更を確認します。

  スキーマについて詳しくは、この [ ページ ](../../configuration/using/data-schemas.md) を参照してください。

* **ワークフロー監査記録**: アクティビティ、ワークフローに最後に加えられた変更およびワークフローの状態を確認します。例えば、次のようなものがあります。

   * 開始
   * 一時停止
   * 停止
   * 再度開始
   * クリーンアップ（「履歴をパージ」アクションと同じ）
   * シミュレーション（「シミュレーションモードで開始」アクションと同じ）
   * ウェイクアップ（「保留中のタスクを今すぐ実行」アクションと同じ）
   * 無条件停止

  ワークフローについて詳しくは、この[ページ](../../workflow/using/about-workflows.md)を参照してください。

  ワークフローの監視方法について詳しくは、[該当する節](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

* **オプション監査記録**: アクティビティと、オプションに最後に加えられた変更を確認します。

  オプションについて詳しくは、この[ページ](../../installation/using/configuring-campaign-options.md)を参照してください。

## 監査記録へのアクセス {#accessing-audit-trail}

インスタンスの **[!UICONTROL 監査記録]** にアクセスするには：

1. インスタンスの&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;メニューにアクセスします。
1. **[!UICONTROL 管理]** メニューで、「**[!UICONTROL 監査]**」を選択します。

   ![](assets/audit_trail_1.png)

1. **[!UICONTROL 監査記録]**&#x200B;ウィンドウが開き、エンティティのリストが表示されます。Adobe Campaignは、ワークフロー、オプションおよびスキーマの作成、編集および削除アクションを監査します。

   最後の変更の詳細を確認するには、いずれかのエンティティを選択します。

   ![](assets/audit_trail_2.png)

1. **[!UICONTROL エンティティを監査]**&#x200B;ウィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL タイプ]**：ワークフロー、オプションまたはスキーマ。
   * **[!UICONTROL エンティティ]**：アクティビティの内部名。
   * **[!UICONTROL 変更者]**：このエンティティを最後に変更したユーザーのユーザー名。
   * **[!UICONTROL アクション]**：このエンティティで最後に実行されたアクション（作成済み、編集済み、または削除済み）。
   * **[!UICONTROL 変更日]**：このエンティティで最後に実行されたアクションの日付。

   コードブロックには、エンティティ内で正確に何が変更されたかについての詳細情報が表示されます。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、**[!UICONTROL 監査ログ]** の保持期間は 180 日に設定されています。 保持期間の変更方法について詳しくは、この [ ページ ](../../production/using/database-cleanup-workflow.md#deployment-wizard) を参照してください。

## 監査記録を有効／無効にする {#enable-disable-audit-trail}

例えば、データベースの容量を節約する場合など、監査記録を特定のアクティビティに対して簡単にアクティブ化または非アクティブ化できます。

それには、次の手順に従います。

1. インスタンスの&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;メニューにアクセスします。
1. **[!UICONTROL 管理]** メニューで **[!UICONTROL Platform]** / **[!UICONTROL オプション]** を選択します。

   ![](assets/audit_trail_4.png)

1. アクティブ化／非アクティブ化するエンティティに応じて、次のオプションのいずれかを選択します。

   * ワークフローの場合：**[!UICONTROL XtkAudit_Workflows]**
   * スキーマの場合：**[!UICONTROL XtkAudit_DataSchema]**
   * オプションの場合：**[!UICONTROL XtkAudit_Option]**
   * すべてのエンティティの場合：**[!UICONTROL XtkAudit_Enable_All]**

   ![](assets/audit_trail_5.png)

1. エンティティを有効にする場合は&#x200B;**[!UICONTROL 値]**&#x200B;を 1 に、無効にする場合は 0 に変更します。

   ![](assets/audit_trail_6.png)

1. **[!UICONTROL 保存]** をクリックします。
