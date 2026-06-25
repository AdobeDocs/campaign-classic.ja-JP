---
product: campaign
title: 外部シグナル
description: 外部シグナルワークフローアクティビティの詳細を説明します
feature: Workflows
hide: true
exl-id: da84d3ff-1e64-45ef-bef0-da4a24d93461
TQID: https://experienceleague.adobe.com/2fWd7-VtAc2x-MQm-o5rpGmDsrn6rszSfZxjVDzleTw
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 171
ht-degree: 100%

---

# 外部シグナル{#external-signal}



「**外部シグナル**」アクティビティを使用して、スケジュールに対して、ワークフロー内のタスクセットの実行をトリガーできます。

「外部シグナル」タスクが有効化されたら、このタスクは無期限に、または指定された期間の終わりまで停止されます。 そのトランジションは、SOAP 呼び出し **PostEvent(sessionToken, workflowId, activity, transition, parameters, complete)** によってアクティブ化されます。**[!UICONTROL complete]** パラメーターを使用すると、後続の呼び出しに反応しないようにタスクを完了できます。

PostEvent 関数について詳しくは、SOAP 呼び出しに関するオンラインドキュメントを参照してください。

このアクティビティを設定して、信号を受信しなかった場合のイベントを定義することができます。 それには、アクティビティを編集し、「**[!UICONTROL 期限]**」タブをクリックします。 「**[!UICONTROL 挿入]**」ボタンをクリックして、イベントを作成して設定します。

![](assets/edit_signal.png)

期限の設定について詳しくは、[有効期限](defining-approvals.md)を参照してください。

「**遅延**」フィールドでは、選択した単位で期限を指定できます。 [待機](wait.md)を参照してください。

各行は、期限のタイプとトランジションとの紐付けを表します。

![](assets/external_sign_diag.png)
