---
product: campaign
title: 分岐
description: 分岐ワークフローアクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: flow-control-activities
exl-id: 7a38653b-c15d-4ed8-85dc-f7214409f42b
source-git-commit: 1113afb573bad958ec7cc2cf008f71c8e751e8f9
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 11%

---

# 分岐{#fork}

![](../../assets/common.svg)

**[!UICONTROL 分岐]** アクティビティを使用して、複数のアウトバウンドトランジションを作成し、同じワークフロー内で複数のアクティビティを個別に実行できます。

>[!IMPORTANT]
>
>**[!UICONTROL 分岐]** アクティビティの後に追加したアウトバウンドトランジションは、同時に実行されません。 この動作は、ワークフローのパフォーマンスに影響を与える可能性があります。 複数のアクティビティを個別に実行する必要がある場合は、**[!UICONTROL 分岐]** アクティビティを使用します。 必要に応じて、ワークフローの後続の部分の前に、アウトバウンドアクティビティを結合できます。

**[!UICONTROL Fork]** アクティビティとその関連アクティビティを設定するには、次の手順に従います。

1. **[!UICONTROL 分岐]** アクティビティを開き、アウトバウンドトランジションの名前とラベルを定義します。

   ![](assets/s_user_segmentation_fork.png)

1. 各アウトバウンドトランジションを開き、設定します。
1. オプションで、アウトバウンドトランジションに参加するには、 AND 結合アクティビティを追加します。 [詳細情報](and-join.md)。

   ワークフローの後続の部分は、結合されたアウトバウンドトランジションの完了時にのみ実行されます。

## 例：セグメント化

この例では、異なる E メールが異なる母集団グループに送信されます。 クエリの後に **[!UICONTROL Fork]** アクティビティを使用して、2 つのアクションを並行して実行します。

* クエリ結果の保存
* 結果をセグメント化して複数の配信を送信

   ![分岐アクティビティは、2 つのクエリの積集合に従い、リスト更新アクティビティと分割アクティビティの前に行われます。](assets/wkf_fork_example.png)

ワークフローは、次のアクティビティで構成されます。

1. **** Queryactivity

   次の 2 つの母集団グループが選択されます。女性とパリ人。

1. **** Intersectionactivity

   クエリ結果の積集合、つまりパリの女性が選択されます。

1. **** Forkactivity

   計算された母集団が保存され、同時に、次の 2 つのグループに分類されます。

   1. 18 歳から 40 歳のパリの女性
   1. 40 歳以上のパリの女性

1. **[!UICONTROL 配信アクティビティ]**

   母集団グループごとに異なる E メールが送信されます。

## 使用例：誕生日の E メールを送る

繰り返し E メールが、誕生日の受信者のリストに送信されます。 **[!UICONTROL 分岐]** アクティビティは、閏年の 2 月 29 日に生まれた受信者を含めるために使用します。 [この使](sending-a-birthday-email.md) 用例の詳細を説明します。

![分岐アクティビティは、テストアクティビティに従い、2 つのクエリアクティビティの前に配置されます。](assets/birthday-workflow_usecase_1.png)

## 使用例：ワークフローでのコンテンツの自動化

コンテンツブロックの作成と配信は自動化されます。 **[!UICONTROL 分岐]** アクティビティを使用してターゲットを計算し、同時にコンテンツを作成します。 [この使](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content) 用例の詳細を説明します。

![分岐アクティビティは、配信アクティビティに従い、クエリアクティビティとコンテンツ管理アクティビティの前に行われます。両方のアクティビティは、AND 結合アクティビティを通じて結合されます。](../../delivery/using/assets/d_ncs_content_workflow10.png)

その後、必要に応じて、各アウトバウンドトランジションを設定し、[AND 結合](and-join.md)アクティビティを使用して結合できます。 このようにして、残りのワークフローは、**[!UICONTROL 分岐]**&#x200B;アクティビティのアウトバウンドトランジションが終了した場合にのみ実行されます。

## 関連トピック

* [AND 結合アクティビティ](and-join.md)
* [使用例：誕生日の E メール](sending-a-birthday-email.md)
* [使用例：コンテンツの作成と配信](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)