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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# ワークフローの管理{#managing-workflows}

デフォルトでは、新しいワークフローは、事前設定済みで受信者テーブル(nms:受信者)に基づくワークフローテンプレートに基づいています。 Nms_DefaultRcpSchema **オプション(「インターフェイスの**[](../../configuration/using/configuring-the-interface.md) 設定」セクションを参照)で参照されているカスタム受信者のテーブルに基づいて、ワークフローを自動的に作成するには、新しいワークフローテンプレートを作成する必要があります。

「 **[!UICONTROL リソース/テンプレート/ワークフローテンプレート]** 」ノードを使用して、新しいテンプレートを作成します。 テンプレートのプロパティで、提供されるディメンションは外部受信者テーブルと一致します。

最近作成したワークフローに基づいて新しいテンプレートを作成すると、パーソナライズされたテーブルが、ワークフローのグローバルターゲット設定とフィルタリングディメンションに対してデフォルトで選択されます。

ワークフローで使用されるすべてのアクティビティは、追加の手動設定を必要とせずに、カスタムテーブルを使用します。

ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

![](assets/cfg_external_table_workflow.png)

