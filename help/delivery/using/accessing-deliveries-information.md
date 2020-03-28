---
title: 配信情報へのアクセス
seo-title: 配信情報へのアクセス
description: 配信情報へのアクセス
seo-description: null
page-status-flag: never-activated
uuid: dc8f0267-1884-4a39-9a7d-d5ef21932928
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: about-deliveries-and-channels
discoiquuid: d2631c67-7781-4baa-b24e-e7921353d131
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 211556bbf023731ffeab2e90692410a852ab3555

---


# 配信情報へのアクセス{#accessing-deliveries-information}

## 配信のリストへのアクセス {#accessing-the-list-of-deliveries}

配信のリストにアクセスするには、**[!UICONTROL キャンペーン]**&#x200B;ウィンドウに移動して、「**[!UICONTROL 配信]**」リンクをクリックします。

[エクスプローラービュー](../../platform/using/adobe-campaign-workspace.md#about-adobe-campaign-explorer)を使用している場合は、ツリーの&#x200B;**[!UICONTROL キャンペーン管理／配信]**&#x200B;ノードから、すべての配信にアクセスできます。

>[!NOTE]
>
>Adobe Campaign のワークスペースについては、[この節](../../platform/using/adobe-campaign-workspace.md)で説明しています。

このページでは、配信の概要を表示できます。ここにはデータベース内のすべての配信が表示され、ステータス、成功率、および変更日を確認できます。

![](assets/d_ncs_user_filter_interface_delivery01.png)

>[!NOTE]
>
>情報のフィルターについては、[この節](../../platform/using/filtering-options.md)で説明しています。

配信ウィザードによって、配信を設定し、承認プロセスを開始して送信できます。ウィザードの内容は、通信チャネル（E メール、モバイル、プッシュ、ダイレクトメール）およびオペレーター権限によって異なります。

リスト内の配信を操作するには、配信をクリックします。新しいウィンドウが開き、例えば、配信を確認したり、一時停止したりできます。

![](assets/s_ncs_user_interface_delivery02.png)

配信サイクルのステージに応じて、主なステータスは次のように表示されます。

* キャンセル済み
* 失敗
* 保留中
* 終了
* 一時停止
* 再試行中
* 処理中
* 配信準備完了
* 準備中
* ターゲットの計算
* 編集中

それぞれのステータスには、独自の色とラベルがあります。

![](assets/s_ncs_user_status_campaigns_120.png)

「**[!UICONTROL 作成]**」ボタンの横にあるドロップダウンリストを使用して、ステータスに基づいて配信をフィルターできます。

![](assets/delivery_filter_status.png)

## 配信カレンダーへのアクセス {#accessing-the-delivery-calendar}

配信カレンダーにアクセスするには、**[!UICONTROL キャンペーン]**&#x200B;ウィンドウに移動して、「**[!UICONTROL キャンペーンカレンダー]**」リンクをクリックします。このカレンダーは、キャンペーンの分類を時系列で表示します。月、週、日単位で表示をパーソナライズできます。

![](assets/s_ncs_user_interface_delivery04.png)

配信の名前をクリックして、配信の主要情報を表示します。必要に応じて、「**[!UICONTROL 開く]**」をクリックしてキャンペーンを開くこともできます。

![](assets/s_ncs_user_interface_delivery05.png)

## 配信スループット情報へのアクセス {#accessing-deliveries-throughput-information}

**[!UICONTROL 配信スループット]**&#x200B;ページの情報は、プラットフォームのすべての配信に関連しています。メッセージが配信される速度を測定するには、1 時間に送信されたメッセージの数とメッセージのサイズ（bps）が基準になります。次の例では、最初のグラフに正常な配信を青で、誤った配信をオレンジで示しています。

スループットを計算する時間枠を選択できます。そのためには、ドロップダウンリストから値を選択して、「**[!UICONTROL 更新]**」をクリックします。

![](assets/s_ncs_user_interface_delivery06.png)

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで Enhanced MTA にアップグレードした場合、**[!UICONTROL 配信スループット]**&#x200B;ページには E メールの受信者へのスループットが表示されなくなります。Campaign から Enhanced MTA へのメッセージのリレーのスループット速度が表示されます。
>
>Adobe Campaign Enhanced MTA について詳しくは、この[ドキュメント](https://helpx.adobe.com/jp/campaign/kb/campaign-enhanced-mta.html)を参照してください。