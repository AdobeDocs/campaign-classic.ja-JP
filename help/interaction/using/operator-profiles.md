---
product: campaign
title: オペレーターのプロファイル
description: オペレーターのプロファイル
feature: Interaction, Offers
audience: interaction
content-type: reference
topic-tags: managing-environments
exl-id: e11fb28c-d530-45a2-862a-ff1c20975577
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: ht
source-wordcount: '408'
ht-degree: 100%

---

# オペレーターのプロファイル{#operator-profiles}



インタラクションを使用するオペレーターには、オファーマネージャーと配信責任者という 2 つのタイプがあります。それぞれが異なる権限を持ち、ツリーやプラットフォームの一部にのみアクセスできます。

* **[!UICONTROL オファーマネージャー]**：オファーを作成して管理します。ワークフローでオファーを使用する場合は、そのワークフローを実行するために、**[!UICONTROL 管理者]**&#x200B;または&#x200B;**[!UICONTROL オファーマネージャー]**&#x200B;のオペレーターグループにオペレーターが属している必要があります。
* **[!UICONTROL 配信責任者]**：オファーの承認と使用

インタラクションに特化したオペレーターを作成する手順は、このプラットフォームの他のすべてのオペレーターを作成する手順と同じです。詳しくは、[この節](../../platform/using/access-management.md)を参照してください。権限は、オペレーターの作成時に設定します。

## オファーマネージャー {#offer-manager}

1. 新しいオペレーターを作成します。
1. **[!UICONTROL グループとネームド権限]**&#x200B;ウィンドウに移動して、「**[!UICONTROL 追加]**」をクリックし、「**[!UICONTROL オファーマネージャー]**」グループを選択します。

   ![](assets/offer_operators_create_001.png)

オファーマネージャーに割り当てられる権限で実行できるタスクは次のとおりです。

* **[!UICONTROL デザイン]**&#x200B;環境を修正する。
* **[!UICONTROL ライブ]**&#x200B;環境を表示する。
* 管理機能（定義済みスペースおよびフィルター）を設定する。
* カテゴリを作成および変更する。
* オファーを作成する。
* オファーの実施要件を設定する。
* オファーを承認する。

  >[!NOTE]
  >
  >オファーマネージャーは、2 つの状況においてのみオファーを承認できます。1 つは、レビュー担当者として割り当てられた人がいない場合です。もう 1 つは、テンプレートの作成を担当するオペレーター（レビュー担当者の割り当て権限を持つ）が、オファーのベースとなるオファーテンプレートで、自分自身をレビュー担当者に指定した場合です。

## 配信マネージャー {#delivery-manager}

1. 新しいオペレーターを作成します。
1. **[!UICONTROL グループとネームド権限]**&#x200B;ウィンドウに移動して、「**[!UICONTROL 追加]**」をクリックし、「**[!UICONTROL 配信責任者]**」グループを選択します。

   ![](assets/offer_operators_create_002.png)

割り当てられた権限で配信マネージャーが実行できるタスクは次のとおりです。

* **[!UICONTROL ライブ]**&#x200B;環境を表示する。
* オファーカテゴリを表示および修正する。
* 自分がレビュー担当者の 1 人として指定されている場合、オファーを承認する。

  >[!NOTE]
  >
  >配信マネージャーがオファーを承認するには、オファーの設定時にレビュー担当者として指定されている必要があります。

## オペレーター別の権限の概要 {#recap-of-rights-according-to-operator}

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>オファーマネージャー（編集）</strong><br /> </td> 
   <td> <strong>オファーマネージャー（ライブ）</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>ツリー構造のレベル</strong><br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 編集対象のオファー／ライブオファー<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信者 - 環境<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> 管理<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> スペース<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> 定義済みオファーフィルター<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> タイポロジ<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> タイポロジルール<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーカタログ<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーカテゴリ<br /> </td> 
   <td> 読み取り／書き込み<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td> <strong>配信責任者（編集）</strong><br /> </td> 
   <td> <strong>配信責任者（ライブ）</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>ツリー構造のレベル</strong><br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 編集対象のオファー／ライブオファー<br /> </td> 
   <td> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> 受信者 - 環境<br /> </td> 
   <td> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> 管理<br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> スペース<br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 定義済みオファーフィルター<br /> </td> 
   <td> 読み取り<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> タイポロジ<br /> </td> 
   <td> 読み取り<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> タイポロジルール<br /> </td> 
   <td> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーカタログ<br /> </td> 
   <td> 読み取り<br /> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーカテゴリ<br /> </td> 
   <td> </td> 
   <td> 読み取り<br /> </td> 
  </tr> 
 </tbody> 
</table>
