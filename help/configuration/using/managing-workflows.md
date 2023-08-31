---
product: campaign
title: ワークフローの管理
description: ワークフローの管理
feature: Workflows, Configuration
role: Data Engineer, Developer
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 617b0050-6b04-4c68-9f63-511baae99f41
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 18%

---

# ワークフローの管理{#managing-workflows}



デフォルトでは、新しいワークフローは、事前に設定され、受信者テーブル (nms:recipient) に基づいているワークフローテンプレートに基づいています。 これらを、 **Nms_DefaultRcpSchema** オプション ( [インターフェイスの設定](../../configuration/using/configuring-the-interface.md) 「 」セクション ) を含めるには、新しいワークフローテンプレートを作成する必要があります。

を使用して新しいテンプレートを作成します。 **[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** ノード。 テンプレートのプロパティで、提供されたディメンションは、外部の受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、ワークフローのグローバルターゲティングおよびフィルタリングディメンションに対して、パーソナライズされたテーブルがデフォルトで選択されます。

ワークフローで使用されるすべてのアクティビティで、追加の手動設定を必要とせずに、カスタムテーブルが使用されます。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)
