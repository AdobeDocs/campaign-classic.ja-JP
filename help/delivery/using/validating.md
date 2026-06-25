---
product: campaign
title: 検証
description: 検証
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Direct Mail
hide: true
exl-id: 42bb395b-b3fe-4d48-8720-5a4cae191984
TQID: https://experienceleague.adobe.com/I31u-kAqMRpzti-bOtfYjrGbwvmsfeEPwWU7kCFLzcQ
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: e95a583b-fcfa-4524-8666-46a29c828119id: c8da4fdd-eb94-4751-a43c-f82733fb2d6eid: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 277
ht-degree: 100%

---

# 検証{#validating}



配信を検証する際のグローバル概念については、[この節](steps-validating-the-delivery.md)で説明しています。

ダイレクトメール配信の出力ファイルは、配信分析中に生成されます。 ファイルの内容は、選択した出力列によって異なります（[抽出ファイル](defining-the-direct-mail-content.md#extraction-file)を参照）。

>[!NOTE]
>
>分析フェーズについて詳しくは、[配信の分析](steps-validating-the-delivery.md#analyzing-the-delivery)で説明しています。

分析フェーズではファイルが生成されますが、受信者に関する情報（配信ログなど）は更新されません。 したがって、このジョブをキャンセルしても問題は発生しません。

分析の結果と、出力ファイルのコンテンツをチェックしてから、「**[!UICONTROL 配信を確定]**」をクリックします。 配信の開始を確認するメッセージが表示されます。

送信を確認すると、指定したファイルへのデータ抽出が開始されます。

![](assets/s_ncs_user_postal_del_send_confirm_postal.png)

その後、アシスタントを閉じて、配信の詳細情報から「**[!UICONTROL 配信]**」タブを開くと、配信ログを参照できます。

配信ログの取得モードは、配信プロパティの「**[!UICONTROL 分析]**」タブで設定できます。

取得モードには次の 2 種類があります。

* **[!UICONTROL メッセージは検証後に送信されたものとみなされます]**（デフォルトのモード）：この機能モードでは、オペレーターが送信を確認すると、すべてのブロードログが更新され（ステータスが「配信保留」から「送信済み」に変化します）、配信は自動的に「**[!UICONTROL 完了]**」に設定されます。
* **[!UICONTROL 結果ファイルに、送信されたメッセージやエラーメッセージが記述されています]**：このモードでは、サービスプロバイダーから送信された外部ファイルを使用してブロードログを更新できます。 その場合、ブロードログのステータスを更新するには、この情報を処理するためのワークフローが必要です。

  >[!NOTE]
  >
  >また、ブロードログが更新されしだい、ユーザーが配信のステータスを「**[!UICONTROL 完了]**」に変更する必要もあります。
