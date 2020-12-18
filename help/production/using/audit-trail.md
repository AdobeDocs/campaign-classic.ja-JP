---
solution: Campaign Classic
product: campaign
title: 監査記録
description: 監査記録
audience: production
content-type: reference
topic-tags: production-procedures
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---


# 監査記録{#audit-trail}

Adobe Campaignでは、**[!UICONTROL 監査証跡]**&#x200B;は、インスタンス内で行われた変更の完全な履歴へのアクセスを提供します。

**[!UICONTROL 監査]** トレーラーは、Adobe Campaignインスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムでキャプチャします。データの履歴にアクセスし、次のような質問に答えるためのセルフサービスの方法が含まれています。ワークフローに対する変更、および最後に更新したユーザー、またはインスタンス内でユーザーが行った操作。

>[!NOTE]
>
>Adobe Campaignは、ユーザーの権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更を監査しません。\
>監査証跡は、そのインスタンスの管理者のみが管理できます。

監査証跡は、次の3つのコンポーネントで構成されます。

* **スキーマ監査証跡**:スキーマに対して行ったアクティビティと最後の変更を確認します。

   スキーマの詳細については、[ページ](../../configuration/using/data-schemas.md)を参照してください。

* **ワークフローの監査証跡**:ワークフローに対するアクティビティと最後の変更、および次のようなワークフローの状態を確認します。

   * 開始
   * 一時停止
   * 停止
   * 再度開始
   * クリーンアップ アクションの削除履歴と等しい
   * シミュレーションモードでのアクション開始と等しいものをシミュレートする
   * アクションに等しいウェイクアップ保留中のタスクを今すぐ実行
   * 無条件停止

   ワークフローの詳細については、[ページ](../../workflow/using/about-workflows.md)を参照してください。

   ワークフローの監視方法について詳しくは、[専用の](../../workflow/using/monitoring-workflow-execution.md)を参照してください。

* **オプションの監査証跡**:アクティビティと、オプションに対して行った最後の変更を確認します。

   オプションの詳細については、[ページ](../../installation/using/configuring-campaign-options.md)を参照してください。

## 監査証跡へのアクセス{#accessing-audit-trail}

インスタンスの&#x200B;**[!UICONTROL 監査証跡]**&#x200B;にアクセスするには：

1. インスタンスの&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;メニューにアクセスします。
1. **[!UICONTROL 管理]**&#x200B;メニューの下で、「**[!UICONTROL 監査]**」を選択します。

   ![](assets/audit_trail_1.png)

1. 「**[!UICONTROL 監査証跡]**」ウィンドウが開き、エンティティのリストが表示されます。 Adobe Campaignは、ワークフロー、オプション、スキーマの作成、編集、削除アクションを監査します。

   エンティティの1つを選択して、最後の変更の詳細を確認します。

   ![](assets/audit_trail_2.png)

1. 「**[!UICONTROL 監査エンティティ]**」ウィンドウには、選択したエンティティに関する次のような詳細情報が表示されます。

   * **[!UICONTROL タイプ]** :ワークフロー、オプションまたはスキーマ。
   * **[!UICONTROL エンティティ]** :アクティビティの内部名。
   * **[!UICONTROL 変更者]** :このエンティティを最後に変更した人のユーザー名です。
   * **[!UICONTROL アクション]** :このエンティティで実行された最後のアクション（作成済み、編集済み、削除済み）。
   * **[!UICONTROL 変更日]** :このエンティティで最後に実行されたアクションの日付。

   コードブロックを使用すると、エンティティで正確に変更された内容に関する詳細な情報が得られます。

   ![](assets/audit_trail_3.png)

>[!NOTE]
>
>デフォルトでは、**[!UICONTROL 監査ログ]**&#x200B;の保存期間は180日に設定されています。 保持期間の変更方法について詳しくは、[ページ](../../production/using/database-cleanup-workflow.md#deployment-wizard)を参照してください。

## 監査証跡{#enable-disable-audit-trail}を有効化/無効化

監査証跡は、特定のアクティビティに対して容易にアクティブ化または非アクティブ化できます。たとえば、データベース上の領域を保存する場合などです。

それには、次の手順に従います。

1. インスタンスの&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;メニューにアクセスします。
1. **[!UICONTROL 管理]**&#x200B;メニューの下で、**[!UICONTROL プラットフォーム]**&#x200B;を選択し、**[!UICONTROL オプション]**&#x200B;を選択します。

   ![](assets/audit_trail_4.png)

1. アクティブ化/非アクティブ化するエンティティに応じて、次のいずれかのオプションを選択します。

   * ワークフローの場合：**[!UICONTROL XtkAudit_ワークフロー]**
   * スキーマの場合：**[!UICONTROL XtkAudit_DataSchema]**
   * オプション：**[!UICONTROL XtkAudit_Option]**
   * すべてのエンティティに対して：**[!UICONTROL XtkAudit_Enable_All]**

   ![](assets/audit_trail_5.png)

1. エンティティを有効にする場合は&#x200B;**[!UICONTROL 値]**&#x200B;を1に、無効にする場合は0に変更します。

   ![](assets/audit_trail_6.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

