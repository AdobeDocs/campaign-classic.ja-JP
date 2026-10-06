---
product: campaign
title: ワークフローの管理
description: ワークフローの管理
feature: Workflows, Configuration
role: Developer
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
exl-id: 617b0050-6b04-4c68-9f63-511baae99f41
TQID: 'https://experienceleague.adobe.com/dpHtLw4PYGg35t-ihmw9LGUSbjgeNloUhGXp9KPJaRU'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 10%
---
# ワークフローの管理{#managing-workflows}



デフォルトでは、新しいワークフローは、事前設定され、受信者テーブル（nms:recipient）に基づくワークフローテンプレートに基づいています。 **Nms_DefaultRcpSchema** オプションで参照されている受信者のカスタムテーブルに基づいて自動的に作成するには、「[ インターフェイス ](../../configuration/using/configuring-the-interface.md)」セクションの設定を参照してください）、新しいワークフローテンプレートを作成する必要があります。

**[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** ノードを使用して、新しいテンプレートを作成します。 テンプレートのプロパティで、指定されたディメンションは外部受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、ワークフローのグローバルターゲティングとフィルタリングディメンションに対して、パーソナライズされたテーブルがデフォルトで選択されます。

したがって、ワークフローで使用されるすべてのアクティビティは、追加の手動設定を必要とせずにカスタムテーブルを使用します。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)
