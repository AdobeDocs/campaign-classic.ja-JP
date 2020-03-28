---
title: セル
seo-title: セル
description: セル
seo-description: null
page-status-flag: never-activated
uuid: 1b18928f-04e1-4268-ab8e-ff74d78599de
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: targeting-activities
discoiquuid: f7187d42-56e9-4681-b172-22abd43ecd29
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# セル{#cells}

「**[!UICONTROL セル]**」アクティビティは、フォームのデータ列内の各種サブセットのビューを提供します。このアクティビティは、サブセットの操作を容易にし、パーソナライゼーションの可能性を拡大しやすいように設計されています。

![](assets/wf_split_cells.png)

ユーザーのニーズに基づく特定のパラメーターを入力することで設定できます。デフォルトでは、各サブセットの詳細は、「**[!UICONTROL 選択]**」タブと「**[!UICONTROL 詳細設定]**」タブ経由で専用ウィンドウに表示されます。以下の例では、フォームは変更されています。オファーと各サブセットの優先度レベルの関連付けを有効にする「**[!UICONTROL データ]**」タブが追加されています。

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

Adobe Campaign の入力フォームのパーソナライゼーションを実行できるのは、エキスパートユーザーに限られます。詳しくは、[この節](../../configuration/using/identifying-a-form.md)を参照してください。
