---
title: ワークフローの管理
seo-title: ワークフローの管理
description: ワークフローの管理
seo-description: null
page-status-flag: never-activated
uuid: 8b6320c0-1aae-4acd-a698-03f9bebd916d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: ee724240-c337-489d-a21b-5f3aec1f247a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# ワークフローの管理{#managing-workflows}

デフォルトでは、新しいワークフローは、事前設定済みで、受信者テーブル(nms:recipient)に基づくワークフローテンプレートに基づいています。 Nms_DefaultRcpSchemaオプションで参照される受信者のカスタムテーブルに基づいて自動的に受け取るには **(「インターフェイスの設定」セ** クションを参照 [](../../configuration/using/configuring-the-interface.md) )、新しいワークフローテンプレートを作成する必要があります。

ノードを使用して新しいテンプレートを作 **[!UICONTROL Resources > Templates > Workflow templates]** 成します。 テンプレートのプロパティで、提供されたディメンションは外部の受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、パーソナライズされたテーブルが、ワークフローのグローバルターゲット化ディメンションとフィルターディメンションに対してデフォルトで選択されます。

ワークフローで使用されるすべてのアクティビティは、追加の手動設定を必要とせずに、カスタムテーブルを使用します。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)

