---
solution: Campaign Classic
product: campaign
title: このユースケースについて
description: 専用のユースケースを通して A/B テストを実行する方法を説明します。
audience: delivery
content-type: reference
topic-tags: a-b-testing
translation-type: ht
source-git-commit: 50a10e16f320a67cb4ad0e31c1cbe8a9365b7887
workflow-type: ht
source-wordcount: '244'
ht-degree: 100%

---


# このユースケースについて {#about-use-case}

このユースケースでは、ターゲティングワークフローを使用して、2 つの E メール配信コンテンツを比較します。どちらの配信でも、メッセージとテキストは同一とし、レイアウトのみを変更します。

ターゲットの母集団は 3 つに分割します。2 つのテストグループと、その他の母集団です。各テストグループに別々のバージョンを配信します。

配信完了から 5 日間の待機期間を設定します。この待機期間の終了後に結果を集め、開封率の最も高いものを見極めます。次に、最もスコアの高い配信コンテンツをスクリプトで復元し、テストグループとして使用しなかった母集団に送信します。

どの配信で最もスコアが高いのかを判断する基準は、個々のニーズに応じて変わる可能性がある点に注意してください。開封率、クリックスルー率、購読率、応答度などが、この判断基準の候補として挙げられます。

また、このユースケースで説明したテストでは 2 つの配信だけしか扱っていませんが、必要に応じてもっと多くのバージョンをテストすることもできます。その場合は、アクティビティをワークフローに追加してください。

このユースケースを実行する主な手順は次のとおりです。

* [手順 1：ターゲティングワークフローの作成](../../delivery/using/a-b-testing-uc-targeting-workflow.md)
* [手順 2：母集団サンプルの設定](../../delivery/using/a-b-testing-uc-population-samples.md)
* [手順 3：2 つの配信テンプレートの作成](../../delivery/using/a-b-testing-uc-delivery-templates.md)
* [手順 4：ワークフローでの配信の設定](../../delivery/using/a-b-testing-uc-configuring-deliveries.md)
* [手順 5：スクリプトの作成](../../delivery/using/a-b-testing-uc-script.md)
* [手順 6：最終配信の定義](../../delivery/using/a-b-testing-uc-final-delivery.md)
* [手順 7：ワークフローの開始](../../delivery/using/a-b-testing-uc-start-workflow.md)
* [手順 8：結果の分析](../../delivery/using/a-b-testing-uc-analyzing.md)

**関連トピック：**

* [A/B テストの概要](../../delivery/using/get-started-a-b-testing.md)
* [A/B テストの設定](../../delivery/using/configuring-a-b-testing.md)
