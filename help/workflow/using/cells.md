---
product: campaign
title: セル
description: セル
feature: Workflows, Targeting Activity
hide: true
exl-id: 7b562dba-7e4b-40a7-91db-7b9379de44ca
TQID: https://experienceleague.adobe.com/hYy1-NOxnpCxVNYLV4QfiLJPec0IAQ4NlNy6RM6pYjA
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 135
ht-degree: 100%

---

# セル{#cells}



「**[!UICONTROL セル]**」アクティビティは、フォームのデータ列内の各種サブセットのビューを提供します。 このアクティビティは、サブセットの操作を容易にし、パーソナライゼーションの可能性を拡大しやすいように設計されています。

![](assets/wf_split_cells.png)

ユーザーのニーズに基づく特定のパラメーターを入力することで設定できます。 デフォルトでは、各サブセットの詳細は、「**[!UICONTROL 選択]**」タブと「**[!UICONTROL 詳細設定]**」タブ経由で専用ウィンドウに表示されます。 以下の例では、フォームは変更されています。オファーと各サブセットの優先度レベルの関連付けを有効にする「**[!UICONTROL データ]**」タブが追加されています。

![](assets/wf_split_cells_with_customization.png)

この設定では、次の情報がワークフローフォームに追加されました（Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／設定／入力フォーム]**&#x200B;ノード）。

```
<container img="nms:miniatures/mini-enrich.png" label="Data">
                <input xpath="@code"/>
                <container xpath="select/node[@alias='@numTest']">
                  <input alwaysActive="true" expr="'long'" type="expr" xpath="@type"/>
                  <input alwaysActive="true" expr="'Priority'" type="expr" xpath="@label"/>
                  <input label="Priority" maxValue="12" minValue="0" type="number"
                         xpath="@value" xpathEditFromType="@type"/>
                </container>
                <container xpath="select/node[@alias='@test']">
                  <input alwaysActive="true" expr="'string'" type="expr" xpath="@type"/>
                  <input alwaysActive="true" expr="'Identifier'" type="expr" xpath="@label"/>
                  <input label="Cell identifier" xpath="@value"/>
                </container>
                <container xpath="select/node[@alias='linkTest']">
                  <input alwaysActive="true" expr="'link'" type="expr" xpath="@type"/>
                  <input alwaysActive="true" expr="'nms:offer'" type="expr" xpath="@dataType"/>
                  <input alwaysActive="true" expr="'Offre'" type="expr" xpath="@label"/>
                  <input computeStringAlias="@valueLabel" label="Offers" notifyPathList="@_cs|@valueLabel"
                         schema="nms:offer" type="linkEdit" xpath="@value"/>
                </container>
```

Adobe Campaign の入力フォームのパーソナライゼーションを実行できるのは、エキスパートユーザーに限られます。 詳しくは、[この節](../../configuration/using/identifying-a-form.md)を参照してください。
