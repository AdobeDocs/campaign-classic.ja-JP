---
title: 監査証跡
seo-title: 監査証跡
description: 監査証跡
seo-description: null
page-status-flag: never-activated
uuid: b96b93b6-e002-4c67-b9ce-b66cdcd395d7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: aa147a8c-9d93-45c8-bb4a-db714739f4c0
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e1937c1ddcbde092a22f4fe8c50d3d72b02cfeed

---


# Audit trail{#audit-trail}

Adobe Campaignでは、インスタン **[!UICONTROL Audit trail]** ス内で行われた変更の完全な履歴にアクセスできます。

**[!UICONTROL Audit trail]** Adobe Campaignインスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムでキャプチャします。 データの履歴にアクセスし、次のような質問に答えるためのセルフサービスの方法が含まれています。ワークフローに対する変更、最終更新者、またはユーザーがインスタンスで行った操作。

>[!NOTE]
>
>Adobe Campaignでは、ユーザーの権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更は監査されません。\
>監査証跡は、インスタンスの管理者のみが管理できます。

監査証跡は、次の3つのコンポーネントで構成されます。

* **スキーマ監査証跡**:アクティビティおよびスキーマに対して行われた最後の変更を確認します。

   For more information on schemas, refer to this [page](../../configuration/using/data-schemas.md).

* **ワークフロー監査証跡**:ワークフローに対して行われたアクティビティと最後の変更を確認し、さらに次のようなワークフローの状態を確認します。

   * 開始
   * 一時停止
   * 停止
   * 再起動
   * アクションと等しいクリーンアップ削除履歴
   * シミュレーションモードで[開始]アクションに等しいシミュレーション
   * アクションに等しいウェイクアップ保留中のタスクを今すぐ実行
   * 無条件停止
   For more information on workflows, refer to this [page](../../workflow/using/about-workflows.md).

   For more on how to monitor workflows, refer to the [dedicated section](../../workflow/using/monitoring-workflow-execution.md).

* **オプション監査証跡**:アクティビティと、オプションに対して行った最後の変更を確認します。

   For more information on options, refer to this [page](../../installation/using/configuring-campaign-options.md).

## 監査証跡へのアクセス {#accessing-audit-trail}

インスタンスのアクセス方 **[!UICONTROL Audit trail]** 法：

1. インスタンスのメ **[!UICONTROL Explorer]** ニューにアクセスします。
1. メニューの下 **[!UICONTROL Administration]** で、を選択しま **[!UICONTROL Audit]** す。

   ![](assets/audit_trail_1.png)

1. エンテ **[!UICONTROL Audit trail]** ィティのリストが表示されたウィンドウが開きます。 Adobe Campaignは、ワークフロー、オプションおよびスキーマの作成、編集および削除アクションを監査します。

   エンティティの1つを選択して、最後の変更の詳細を確認します。

   ![](assets/audit_trail_2.png)

1. このウ **[!UICONTROL Audit entity]** ィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL Type]** :ワークフロー、オプションまたはスキーマを参照してください。
   * **[!UICONTROL Entity]** :アクティビティの内部名。
   * **[!UICONTROL Modified by]** :このエンティティを最後に修正したユーザー名。
   * **[!UICONTROL Action]** :このエンティティに対して実行された最後のアクション（作成済み、編集済み、削除済み）。
   * **[!UICONTROL Modification date]** :このエンティティで最後に実行されたアクションの日付。
   コードブロックは、エンティティ内で正確に変更された内容に関する詳細情報を提供します。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、のリテンション期間は180日に設定されていま **[!UICONTROL Audit logs]** す。 リテンション期間の変更方法の詳細については、このページを参照してく [ださい](../../production/using/database-cleanup-workflow.md#deployment-wizard)。

## 監査証跡の有効化/無効化 {#enable-disable-audit-trail}

監査証跡は、特定のアクティビティに対して簡単にアクティブ化または非アクティブ化できます。例えば、データベース上に空き領域を保存する場合などです。

これをおこなうには：

1. インスタンスのメ **[!UICONTROL Explorer]** ニューにアクセスします。
1. メニューの **[!UICONTROL Administration]** 下で、を選択し **[!UICONTROL Platform]** てから **[!UICONTROL Options]** 、

   ![](assets/audit_trail_4.png)

1. アクティブ化/非アクティブ化するエンティティに応じて、次のオプションのいずれかを選択します。

   * ワークフローの場合： **[!UICONTROL XtkAudit_Workflows]**
   * スキーマの場合： **[!UICONTROL XtkAudit_DataSchema]**
   * オプション： **[!UICONTROL XtkAudit_Option]**
   * すべてのエンティティに対して： **[!UICONTROL XtkAudit_Enable_All]**
   ![](assets/audit_trail_5.png)

1. エンティティ **[!UICONTROL Value]** を有効にする場合は1に、無効にする場合は0に変更します。

   ![](assets/audit_trail_6.png)

1. クリック **[!UICONTROL Save]** .

