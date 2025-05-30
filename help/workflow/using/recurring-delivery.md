---
product: campaign
title: 繰り返し配信
description: 繰り返し配信ワークフローアクティビティの詳細を説明します
feature: Workflows
hide: true
hidefromtoc: true
exl-id: efd2cdfb-2e5f-4672-8be8-a424481b11ed
source-git-commit: 776c664a99721063dce5fa003cf40c81d94f8c78
workflow-type: ht
source-wordcount: '290'
ht-degree: 100%

---

# 繰り返し配信{#recurring-delivery}

「**[!UICONTROL 繰り返し配信]**」アクティビティでは、キャンペーン固有の配信テンプレートの発生件数を設定できます。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](#recurring-delivery-video)

このアクティビティは、キャンペーン内の「**[!UICONTROL ターゲティングとワークフロー]**」タブでのみ使用できます。

手順は次のとおりです。

1. アクティビティのベースにする配信テンプレートを選択します。

   ![](assets/recurring_delivery_001.png)

1. 配信テンプレートを設定します。

このアクティビティの設定プロセスで使用できるオプションは、配信テンプレートの作成プロセスで使用できるオプションとほぼ同じです。詳しくは、[この節](../../delivery/using/about-templates.md)を参照してください。

>[!CAUTION]
>
>繰り返し配信では、コンテンツのプレビューや、[ターゲットデータ](../../workflow/using/data-life-cycle.md#target-data)のパーソナライゼーション要素を含む配達確認の送信はサポートされていません。

このアクティビティの使用例については、この[節](sending-a-birthday-email.md#creating-a-recurring-delivery-in-a-targeting-workflow)を参照してください。

## 繰り返し配信の設定方法 {#set-up-recurring-delivery}

**繰り返し配信**&#x200B;では、実行のたびに新しい配信インスタンスを作成します。例えば、ワークフローが週に 1 回実行されるようにスケジュールされている場合、1 年後には 52 回の配信が行われることになります。また、broadLog とトラッキングログは、各配信インスタンスで区切られます。

![繰り返し配信](assets/delivery_recurring.jpg)

繰り返し配信の実行を停止する場合は、キャンペーンを完全にキャンセルするか、キャンペーンの実行ワークフローを停止する必要があります。Campaign ダッシュボードから配信を停止すると、配信の発生は停止されます：繰り返し配信の次回のインスタンスは、ワークフローの実行のたびに作成され続けます。

>[!NOTE]
>
>「**[!UICONTROL 繰り返し配信]**」タイプアクティビティから配達確認を送信することはできません。
> 
>キャンペーンワークフロー経由で配信を直接作成するには、事前設定されたチャネル固有のアクティビティを使用します（「**[!UICONTROL 繰り返し配信]**」など）。

## チュートリアルビデオ {#recurring-delivery-video}

このビデオでは、繰り返し配信とスケジューラーアクティビティを設定する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/27508?quality=12&captions=jpn)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
