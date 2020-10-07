---
title: 監査記録
seo-title: 監査記録
description: 監査記録
seo-description: null
page-status-flag: never-activated
uuid: b96b93b6-e002-4c67-b9ce-b66cdcd395d7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: aa147a8c-9d93-45c8-bb4a-db714739f4c0
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 監査記録{#audit-trail}

Adobe Campaignでは、 **[!UICONTROL 監査証跡]** (Audit trail)を使用すると、インスタンス内で行われた変更の完全な履歴にアクセスできます。

**[!UICONTROL 監査証跡]** :Adobe Campaign・インスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムでキャプチャします。 データの履歴にアクセスし、次のような質問に答えるためのセルフサービスの方法が含まれています。ワークフローに対する変更、および最後に更新したユーザー、またはインスタンス内でユーザーが行った操作。

>[!NOTE]
>
>Adobe Campaignは、ユーザーの権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更を監査しません。\
>監査証跡は、そのインスタンスの管理者のみが管理できます。

監査証跡は、次の3つのコンポーネントで構成されます。

* **スキーマ監査証跡**:スキーマに対して行ったアクティビティと最後の変更を確認します。

   For more information on schemas, refer to this [page](../../configuration/using/data-schemas.md).

* **ワークフローの監査証跡**:ワークフローに対するアクティビティと最後の変更、および次のようなワークフローの状態を確認します。

   * 開始
   * 一時停止
   * 停止
   * 再度開始
   * クリーンアップ アクションの削除履歴と等しい
   * シミュレーションモードでのアクション開始と等しいものをシミュレートする
   * アクションに等しいウェイクアップ保留中のタスクを今すぐ実行
   * 無条件停止

   For more information on workflows, refer to this [page](../../workflow/using/about-workflows.md).

   For more on how to monitor workflows, refer to the [dedicated section](../../workflow/using/monitoring-workflow-execution.md).

* **オプションの監査証跡**:アクティビティと、オプションに対して行った最後の変更を確認します。

   For more information on options, refer to this [page](../../installation/using/configuring-campaign-options.md).

## 監査証跡へのアクセス {#accessing-audit-trail}

インスタンスの **[!UICONTROL 監査証跡にアクセスするには]** :

1. インスタンスの **[!UICONTROL Explorer]** メニューにアクセスします。
1. 「 **[!UICONTROL 管理]** 」メニューの「 **[!UICONTROL 監査]** 」を選択します。

   ![](assets/audit_trail_1.png)

1. 「 **[!UICONTROL 監査証跡]** 」ウィンドウが開き、エンティティのリストが表示されます。 Adobe Campaignは、ワークフロー、オプション、スキーマの作成、編集、削除アクションを監査します。

   エンティティの1つを選択して、最後の変更の詳細を確認します。

   ![](assets/audit_trail_2.png)

1. 「 **[!UICONTROL 監査エンティティ]** 」ウィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL タイプ]** :ワークフロー、オプションまたはスキーマ。
   * **[!UICONTROL エンティティ]** :アクティビティの内部名。
   * **[!UICONTROL 変更者]** :このエンティティを最後に変更した人のユーザー名です。
   * **[!UICONTROL アクション]** :このエンティティで実行された最後のアクション（作成済み、編集済み、削除済み）。
   * **[!UICONTROL 変更日]** :このエンティティで最後に実行されたアクションの日付。

   コードブロックを使用すると、エンティティで正確に変更された内容に関する詳細な情報が得られます。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、 **[!UICONTROL 監査ログの保存期間は180日に設定されています]** 。 保持期間の変更方法の詳細については、この [ページを参照してください](../../production/using/database-cleanup-workflow.md#deployment-wizard)。

## 監査証跡の有効化/無効化 {#enable-disable-audit-trail}

監査証跡は、特定のアクティビティに対して容易にアクティブ化または非アクティブ化できます。たとえば、データベース上の領域を保存する場合などです。

それには、次の手順に従います。

1. インスタンスの **[!UICONTROL Explorer]** メニューにアクセスします。
1. 「 **[!UICONTROL 管理]** 」メニューで、「 **[!UICONTROL プラットフォーム]** 」、「 **[!UICONTROL オプション」の順に選択します]** 。

   ![](assets/audit_trail_4.png)

1. アクティブ化/非アクティブ化するエンティティに応じて、次のいずれかのオプションを選択します。

   * ワークフローの場合： **[!UICONTROL XtkAudit_ワークフロー]**
   * スキーマの場合： **[!UICONTROL XtkAudit_DataSchema]**
   * オプション： **[!UICONTROL XtkAudit_Option]**
   * すべてのエンティティに対して： **[!UICONTROL XtkAudit_Enable_All]**

   ![](assets/audit_trail_5.png)

1. エンティティを有効にする場合は **[!UICONTROL 値]** を1に、無効にする場合は0に変更します。

   ![](assets/audit_trail_6.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

