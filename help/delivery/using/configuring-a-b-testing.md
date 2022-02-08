---
product: campaign
title: A/B テストの設定
description: Campaign Classic で A/B テストを設定する方法を説明します。
feature: A/B Testing
exl-id: 6adf2e75-63b1-44ad-8925-03beb3bc0bdd
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 100%

---

# A/B テストの設定 {#configuring-a-b-testing}

![](../../assets/common.svg)

ここでは、A/B テストを実行するワークフローを構築する方法について説明します。

1. 新しいワークフローを作成し、目的の母集団をターゲティングする[クエリ](../../workflow/using/query.md)アクティビティを設定します。

1. [分割](../../workflow/using/split.md)アクティビティを追加して、ターゲット母集団を複数のサブセットに分割します。

1. アクティビティを開き、必要に応じて各サブセットを設定します。**[!UICONTROL 分割]**&#x200B;アクティビティの設定方法の詳細については、[こちらの節](../../workflow/using/split.md)を参照してください。

   この例では、ニュースレター用の 2 つの新しい件名を、それぞれターゲット母集団の 10%に提示して、テストをおこないます。

   ![](assets/ab-testing-split.png)

1. その他の母集団に、現在の件名でニュースレターを送信するためにトランジションを追加します。これをおこなうには、「**[!UICONTROL 一般]**」タブの「**[!UICONTROL 補集合を生成]**」オプションを有効にします。

   ![](assets/ab-testing-complement.png)

1. サブセットごとに、テストする配信のバージョンを追加します。

   ![](assets/ab-testing-delivery.png)

これで、ワークフローを開始できます。配信が送信されると、3 つのサブセットの動作を配信ログでトラッキングして、どの件名が最も成功したかを確認できます。

また、ワークフローを使用すると、プロセスの自動化が可能です。より良いパフォーマンスを示した配信バリアントを自動的に識別して、その他の母集団に送信できます。詳しくは、この専用の[ユースケース](a-b-testing-use-case.md)を参照してください。
