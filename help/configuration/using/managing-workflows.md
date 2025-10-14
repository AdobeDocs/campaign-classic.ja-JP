---
product: campaign
title: ワークフローの管理
description: ワークフローの管理
feature: Workflows, Configuration
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 617b0050-6b04-4c68-9f63-511baae99f41
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 16%

---

# ワークフローの管理{#managing-workflows}



デフォルトでは、新しいワークフローは、事前に設定された受信者テーブル（nms:recipient）に基づくワークフローテンプレートに基づきます。 **Nms_DefaultRcpSchema** オプション（「[&#x200B; インターフェイスの設定 &#x200B;](../../configuration/using/configuring-the-interface.md)」セクションを参照）で参照される受信者のカスタムテーブルに基づいて受信者を自動的に設定するには、新しいワークフローテンプレートを作成する必要があります。

**[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** ノードから新しいテンプレートを作成します。 テンプレートのプロパティで提供されるディメンションは、外部受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、ワークフローのグローバルターゲティングおよびフィルタリングディメンション用に、デフォルトでパーソナライズされたテーブルが選択されます。

したがって、ワークフローで使用されるすべてのアクティビティでは、追加の手動設定を必要とせずに、カスタムテーブルが使用されます。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)
