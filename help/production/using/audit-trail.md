---
product: campaign
title: 監査記録
description: Campaign 監査記録を使用してインスタンスを監視する方法について説明します
feature: Audit Trail, Monitoring, Workflows
exl-id: 8508d879-fb38-4b1f-9f55-0341bb8d0c67
source-git-commit: 3d1ed85dcafc5afc4088db98c09d78fb7e9c0a39
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 85%

---

# 監査記録{#audit-trail}

>[!INFO]
>
>監査記録機能について詳しくは、[Adobe Campaign v8 ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/audit-trail) を参照してください。

Adobe Campaignでは、**[!UICONTROL 監査記録]** を使用すると、インスタンス内で行われた変更の全履歴にアクセスできます。

**[!UICONTROL 監査記録]** は、Adobe Campaign インスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで記録します。 これには、データの履歴を確認することにより、ワークフローで発生した事象、ワークフローの最終更新者、インスタンス内でユーザーが行った操作などを知るのに役立つセルフサービス式の方法が含まれています。

>[!NOTE]
>
>Adobe Campaign では、ユーザー権限、テンプレート、パーソナライゼーションまたはキャンペーン内で行われた変更を監査しません。\
>監査記録は、インスタンスの管理者のみが管理できます。

![](assets/audit_trail_2.png)

+++ 監査記録が使用可能なエンティティについて説明します

* **スキーマ監査記録**：スキーマに行った変更を調べて、変更を行ったユーザーとタイミングを特定できます。

  スキーマについて詳しくは、この [ ページ ](../../configuration/using/data-schemas.md) を参照してください。

* **ワークフロー監査記録**&#x200B;では、以下を含む、ワークフローに関連するすべてのアクションを追跡します。

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

* **オプション監査記録**&#x200B;では、アクティビティと、オプションに最後に行った変更を確認できます。

  オプションについて詳しくは、この[ページ](../../installation/using/configuring-campaign-options.md)を参照してください。

* **配信監査記録**&#x200B;では、アクティビティと、配信に最後に行った変更を確認できます。

  配信について詳しくは、この[ページ](../../delivery/using/communication-channels.md)を参照してください。

* **外部アカウント**&#x200B;では、テクニカルワークフローやキャンペーンワークフローなどの技術プロセスで使用される、外部アカウントに行った変更を確認できます。

  外部アカウントについて詳しくは、この[ページ](../../installation/using/external-accounts.md)を参照してください。

* **配信マッピング**&#x200B;では、配信マッピングに対して行ったアクティビティと最新の変更を監視できます。

  配信マッピングについて詳しくは、この[ページ](../../configuration/using/target-mapping.md)を参照してください。

* **Web アプリケーション**&#x200B;では、入力フィールドと選択フィールドを含むページの作成に使用される Campaign V8 の web フォームに行った変更を確認できます。これには、データベースのデータが含まれている場合があります。

  Web アプリケーションについて詳しくは、この[ページ](../../web/using/about-web-applications.md)を参照してください。

* **オファー**&#x200B;では、アクティビティと、オファーに最後に行った変更を確認できます。

  オファーについて詳しくは、この[ページ](../../interaction/using/interaction-and-offer-management.md)を参照してください。

* **オペレーター**&#x200B;では、アクティビティと、オペレーターに行った最新の変更を監視できます。

  オペレーターについて詳しくは、この[ページ](../../platform/using/access-management-operators.md)を参照してください。

+++
