---
product: campaign
title: ワークフローの管理
description: ワークフローの管理
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 617b0050-6b04-4c68-9f63-511baae99f41
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---

# ワークフローの管理{#managing-workflows}

![](../../assets/v7-only.svg)

デフォルトでは、新しいワークフローは、事前設定され、受信者テーブル (nms:recipient) に基づいたワークフローテンプレートに基づいています。 **Nms_DefaultRcpSchema** オプションで参照される受信者のカスタムテーブルに基づいて自動的に受信を行うには（[ インターフェイスの設定 ](../../configuration/using/configuring-the-interface.md) の節を参照）、新しいワークフローテンプレートを作成する必要があります。

**[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** ノードを使用して、新しいテンプレートを作成します。 テンプレートのプロパティで、提供されたディメンションは、外部の受信者テーブルと一致します。

最近作成したテンプレートに基づいて新しいワークフローを作成すると、ワークフローのグローバルターゲティングおよびフィルタリングディメンションに対して、パーソナライズされたテーブルがデフォルトで選択されます。

ワークフローで使用されるすべてのアクティビティで、追加の手動設定を必要とせずに、カスタムテーブルが使用されます。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)
