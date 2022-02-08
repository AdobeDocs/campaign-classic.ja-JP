---
product: campaign
title: キャンペーンタイポロジについて
description: キャンペーンタイポロジについて
feature: Typology Rules
topic-tags: campaign-optimization
exl-id: 6d5b8584-4aa1-4d9a-89d9-d41da75dd323
source-git-commit: 8fa50d17a9ff36ccc310860ac93771590cfd76fd
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 100%

---

# キャンペーンタイポロジについて{#about-campaign-typologies}

![](../../assets/common.svg)

キャンペーンの最適化は、配信状況を制御、フィルターおよび監視する Adobe Campaign のモジュールです。キャンペーン間の競合を回避するために、Adobe Campaign では特定の制限ルールを適用して、様々な組み合わせをテストできます。このテストにより、企業のコミュニケーションポリシーに準拠し、顧客のニーズと期待に応える最適なメッセージを送信できます。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](#typologies-video)

>[!NOTE]
>
>提供されている内容によって、キャンペーンの最適化は含まれていることも、アドインになっていることもあります。使用許諾契約書を確認してください。

## タイポロジルール {#typology-rules}

Adobe Campaign では、次の 4 種類のタイポロジルールをデザインおよび適用できます。

* **フィルター**&#x200B;ルール：条件に基づいて、ターゲットの一部を除外します。詳しくは、[フィルタールール](filtering-rules.md)を参照してください。
* **頻度**&#x200B;ルール： マーケティング疲労（過剰なマーケティングによる弊害）を抑制します。詳しくは、[頻度ルール](pressure-rules.md)を参照してください。
* **処理能力**&#x200B;ルール：最適な処理環境を確保するために、負荷を制限します。詳しくは、[処理能力の制御](consistency-rules.md#controlling-capacity)を参照してください。
* **コントロール**&#x200B;ルール：メッセージを送信する前にメッセージの有効性を確認します。詳しくは、[コントロールルール](control-rules.md)を参照してください。

作成されたタイポロジルールは、キャンペーンタイポロジでグループ化され、配信で参照されます。[タイポロジの適用](#applying-typologies)を参照してください。

## タイポロジ {#typologies}

キャンペーンタイポロジには、複数の[タイポロジルール](#typology-rules)を含めることができますが、1 つの配信では 1 つのタイポロジしか参照できません。

「**[!UICONTROL ルール]**」タブでは、適用するタイポロジルールを追加、削除、表示できます。

![](assets/campaign_opt_rules_tab.png)

## タイポロジの適用 {#applying-typologies}

以下に、タイポロジを作成して配信に適用する手順を示します。

1. タイポロジルールを作成する。

   タイポロジルールは、**[!UICONTROL 管理／キャンペーン管理／タイポロジ管理／タイポロジルール]**&#x200B;ノードで表示できます。

   Campaign で使用できる様々なルールについて詳しくは、[営業頻度ルール](pressure-rules.md)、[処理能力ルール](consistency-rules.md#controlling-capacity)、[コントロールルール](control-rules.md)および[フィルタールール](filtering-rules.md)を参照してください。

1. タイポロジを作成し、作成したルールをその中で参照する。

   タイポロジにアクセスするには、**[!UICONTROL 管理／キャンペーン管理／タイポロジ管理／]****[!UICONTROL タイポロジ]**&#x200B;ノードに移動します。

1. 作成したタイポロジを使用するように配信を設定します。詳しくは、[この節](applying-rules.md#applying-a-typology-to-a-delivery)を参照してください。
1. キャンペーンのシミュレーションによって動作をテストして制御する。キャンペーンのシミュレーションについて詳しくは、[この節](campaign-simulations.md)を参照してください。

配信の準備では、基準を満たした場合に受信者が除外されます。ログを確認して除外を監視することができます。頻度タイポロジルールの使用例については、[このページ](pressure-rules.md#use-cases-on-pressure-rules)を参照してください。

## チュートリアルビデオ {#typologies-video}

### タイポロジルールを使用した疲労管理の設定方法

このビデオでは、タイポロジルールを活用して Adobe Campaign で疲労管理を実装する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25090?quality=12)

### 定義済みフィルターを使用した疲労管理の設定方法

疲労管理では、受信者の過剰勧誘を避けるために、メッセージの頻度と数量を制御します。キャンペーンインスタンスにキャンペーン最適化モジュールがない場合、受信したメッセージの数でターゲット母集団をフィルタリングする定義済みフィルターを設定できます。
このビデオでは、フィルターを使用して Adobe Campaign Classic で疲労管理を実装する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25091?quality=12)

Campaign に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。

**関連トピック**

* [任意のチャネルの配信に対する自動ビジネスルールの適用](https://helpx.adobe.com/jp/campaign/kb/simplifying-campaign-management-acc.html#Applyautomaticbusinessrulestodeliveriesonanychannel)

* [タイポロジと疲労管理の概要](pressure-rules.md)

