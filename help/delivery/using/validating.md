---
title: 検証
seo-title: 検証
description: 検証
seo-description: null
page-status-flag: never-activated
uuid: e3cd96ef-4f5d-4e17-9fec-5eaa4d835cb1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-direct-mail
discoiquuid: c363a7cf-81a5-4c02-a021-b822eeeadd03
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 70f51ba3937d0f20d9a488c61b52b7ec4396fa5e

---


# 検証{#validating}

配信を検証する際のグローバル概念については、この節 [で説明します](../../delivery/using/steps-validating-the-delivery.md)。

ダイレクトメール配信の出力ファイルは、配信分析中に生成される。 ファイルの内容は、選択した出力列によって異なります( [抽出ファイル](../../delivery/using/defining-the-direct-mail-content.md#extraction-file))。

>[!NOTE]
>
>分析フェーズの詳細は、配信の分 [析を参照してください](../../delivery/using/steps-validating-the-delivery.md#analyzing-the-delivery)。

分析フェーズではファイルが生成されますが、受信者に関する情報（配信ログなど）は更新されません。したがって、このジョブをキャンセルしても問題は発生しません。

Check the result of the analysis and the content of the output file before clicking **[!UICONTROL Confirm delivery]**. 配信の開始を確認するメッセージが表示されます。

送信を確認すると、指定したファイルへのデータ抽出が開始されます。

![](assets/s_ncs_user_postal_del_send_confirm_postal.png)

You can then close the wizard and look at the delivery logs via the **[!UICONTROL Delivery]** tab, accessible via the delivery details.

You can configure the delivery logs retrieval mode from the **[!UICONTROL Analysis]** tab of the delivery properties.

取得モードには次の 2 種類があります。

* **[!UICONTROL Messages are considered sent after validation]** （デフォルトモード）:この機能モードでは、オペレータが送信を確認し（ステータスが「配信待ち」から「送信済み」に変わり）、配信が自動的ににに設定されると、すべてのブロードログが更新されま **[!UICONTROL Finished]**&#x200B;す。
* **[!UICONTROL A file of results determines the messages that are sent and those that have failed]** :このモードを使用すると、サービスプロバイダーから送信された外部ファイルを介してブロードログを更新できます。 その場合、ブロードログのステータスを更新するには、この情報を処理するためのワークフローが必要です。

   >[!NOTE]
   >
   >In this case, the delivery&#39;s status also needs to be changed to **[!UICONTROL Finished]** by the user as soon as the broadlogs are updated.
