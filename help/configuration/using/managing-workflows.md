---
product: campaign
title: ワークフローの管理
description: ワークフローの管理
feature: Workflows, Configuration
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 617b0050-6b04-4c68-9f63-511baae99f41
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 16%

---

# ワークフローの管理{#managing-workflows}



デフォルトでは、新しいワークフローは、事前設定され、受信者テーブル（nms:recipient）に基づくワークフローテンプレートに基づいています。 **Nms_DefaultRcpSchema** オプションで参照されている受信者のカスタムテーブルに基づいて自動的に作成するには、「[&#x200B; インターフェイス &#x200B;](../../configuration/using/configuring-the-interface.md)」セクションの設定を参照してください）、新しいワークフローテンプレートを作成する必要があります。

**[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** ノードを使用して、新しいテンプレートを作成します。 テンプレートのプロパティで、指定されたディメンションは外部受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、ワークフローのグローバルターゲティングとフィルタリングディメンションに対して、パーソナライズされたテーブルがデフォルトで選択されます。

したがって、ワークフローで使用されるすべてのアクティビティは、追加の手動設定を必要とせずにカスタムテーブルを使用します。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)
