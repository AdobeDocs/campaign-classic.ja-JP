---
solution: Campaign Classic
product: campaign
title: この使用例について
description: 専用の使用例を通してA/Bテストを実行する方法を学びます。
audience: delivery
content-type: reference
topic-tags: a-b-testing
translation-type: tm+mt
source-git-commit: 346b72d522c947b2a2552176b910ded8d622f3ab
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 52%

---


# この使用例について {#about-use-case}

この使用例では、ターゲティングワークフローを使用して、2 つの E メール配信コンテンツを比較します。どちらの配信でも、メッセージとテキストは同一とし、レイアウトのみを変更します。

ターゲットの母集団は 3 つに分割します。2 つのテストグループと、その他の母集団です。各テストグループに別々のバージョンを配信します。

配信完了から 5 日間の待機期間を設定します。この待機期間の終了後に結果を集め、開封率の最も高いものを見極めます。次に、スコアが最も高い配信の内容がスクリプトによって回復され、テストグループとして使用されていない訪問者に送信されます。

どの配信で最もスコアが高いのかを判断する基準は、個々のニーズに応じて変わる可能性がある点に注意してください。開封率、クリックスルー率、購読率、応答度などが、この判断基準の候補として挙げられます。

さらに、この使用事例で詳しく説明するテストは2つの配信に関するものに限られますが、必要な数のバージョンをテストできます。 その場合は、単にアクティビティをワークフローに追加するだけです。

この使用例を実行する主な手順は次のとおりです。

* [手順1:ターゲット設定ワークフローの作成](#step-1--creating-a-targeting-workflow)
* [手順2:母集団サンプルの設定](#step-2--configuring-population-samples)
* [手順3:2つの配信テンプレートを作成](#step-3--creating-two-delivery-templates)
* [手順4:ワークフローでの配信の設定](#step-4--configuring-the-deliveries-in-the-workflow)
* [手順5:スクリプトの作成](#step-5--creating-the-script)
* [手順7:ワークフローの開始](#step-7--starting-the-workflow)
* [手順8:結果を分析します](#step-8--analyzing-the-result)。

**関連トピック：**

* [A/Bテストを始める](../../delivery/using/get-started-a-b-testing.md)
* [A/Bテストの設定](../../delivery/using/configuring-a-b-testing.md)
