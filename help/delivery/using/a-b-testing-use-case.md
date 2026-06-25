---
product: campaign
title: A/B テストのユースケース
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: 4eb139a0-5342-4084-9f6d-d736e05bf1c6
TQID: https://experienceleague.adobe.com/rYG71DezWYLaFpxjPKrnCEQJgyDVjFfopNsr6aWtQ1w
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 267
ht-degree: 100%

---

# A/B テスト：このユースケースに対する A/B テスト {#ab-testing-use-case}

このユースケースでは、ターゲティングワークフローを使用して、2 つのメール配信コンテンツを比較します。 どちらの配信でも、メッセージとテキストは同一とし、レイアウトのみを変更します。

ターゲットの母集団は、2 つのテストグループと、その他の母集団の 3 つに分割します。 各テストグループに別々のバージョンを配信します。

配信完了から 5 日間の待機期間を設定します。この待機期間の終了後に結果を集め、開封率の最も高いものを見極めます。 次に、最もスコアの高い配信コンテンツをスクリプトで復元し、テストグループとして使用しなかった母集団に送信します。

どの配信で最もスコアが高いのかを判断する基準は、個々のニーズに応じて変わる可能性がある点に注意してください。 開封率、クリックスルー率、購読率、応答度などが、この判断基準の候補として挙げられます。

また、このユースケースで説明したテストでは 2 つの配信だけしか扱っていませんが、必要に応じてもっと多くのバージョンをテストすることもできます。 その場合は、アクティビティをワークフローに追加してください。

このユースケースを実行する主な手順は次のとおりです。

* [手順 1：ターゲティングワークフローの作成](a-b-testing-uc-targeting-workflow.md)
* [手順 2：母集団サンプルの設定](a-b-testing-uc-population-samples.md)
* [手順 3：2 つの配信テンプレートの作成](a-b-testing-uc-delivery-templates.md)
* [手順 4：ワークフローでの配信の設定](a-b-testing-uc-configuring-deliveries.md)
* [手順 5：スクリプトの作成](a-b-testing-uc-script.md)
* [手順 6：最終配信の定義](a-b-testing-uc-final-delivery.md)
* [手順 7：ワークフローの開始](a-b-testing-uc-start-workflow.md)
* [手順 8：結果の分析](a-b-testing-uc-analyzing.md)

**関連トピック：**

* [A/B テストの基本を学ぶ](get-started-a-b-testing.md)
* [A/B テストの設定](configuring-a-b-testing.md)
