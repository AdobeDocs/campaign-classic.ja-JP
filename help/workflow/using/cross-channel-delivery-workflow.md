---
product: campaign
title: クロスチャネル配信ワークフロー
description: クロスチャネル配信ワークフローの詳細を説明します
feature: Workflows, Channels Activity
hide: true
hidefromtoc: true
exl-id: dfd36d2c-44ff-49a9-80b4-09eaf3377072
source-git-commit: 776c664a99721063dce5fa003cf40c81d94f8c78
workflow-type: ht
source-wordcount: '762'
ht-degree: 100%

---

# クロスチャネル配信ワークフロー{#cross-channel-delivery-workflow}



この使用例では、クロスチャネル配信ワークフローに関する例を示します。クロスチャネル配信の一般的な概念については、[この節](cross-channel-deliveries.md)で説明しています。

ここでは、1 つのグループにメールを送信し、もう 1 つのグループに SMS メッセージを送信することを目的に、データベースの受信者からオーディエンスを別々のグループにセグメント化します。

この使用例の主な実装手順は次のとおりです。

1. オーディエンスをターゲットとする&#x200B;**[!UICONTROL クエリ]**&#x200B;アクティビティを作成する。
1. **[!UICONTROL オファーへのリンクを含むメール配信]**&#x200B;アクティビティを作成する。
1. **[!UICONTROL 分割]**&#x200B;アクティビティを使用して、以下を実行する。

   * 最初のメールを開封しなかった受信者に別のメールを送信する。
   * メールを開封したが、オファーへのリンクをクリックしなかった受信者に SMS を送信する。
   * メールを開封し、オファーへのリンクをクリックした受信者をデータベースに追加する。

![](assets/wkf_cross-channel_7.png)

## 手順 1：オーディエンスのターゲティング {#step-1--targeting-the-audience}

ターゲットを定義するために、受信者を特定するクエリを作成します。

1. キャンペーンを作成します。詳しくは、[この節](../../campaign/using/setting-up-marketing-campaigns.md#creating-a-campaign)を参照してください。
1. キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブで、ワークフローに&#x200B;**クエリ**&#x200B;アクティビティを追加します。このアクティビティの使用について詳しくは、[この節](query.md)を参照してください。
1. 配信を受信する受信者を定義します。例えば、ターゲットディメンションとして「ゴールド」メンバーを選択します。
1. クエリにフィルター条件を追加します。この例では、メールアドレスと携帯電話番号を持つ受信者を選択します。

   ![](assets/wkf_cross-channel_3.png)

1. 変更を保存します。

## 手順 2：オファーを含んだメールの作成 {#step-2--creating-an-email-including-an-offer}

1. **[!UICONTROL メール配信]**&#x200B;アクティビティを作成し、ワークフローでそのアクティビティをダブルクリックして、編集します。メールの作成について詳しくは、[この節](../../delivery/using/about-email-channel.md)を参照してください。
1. メッセージをデザインし、オファーを含むリンクをコンテンツに挿入します。

   ![](assets/wkf_cross-channel_1.png)

   メッセージ本文へのオファーのビルトインについて詳しくは、[この節](../../interaction/using/integrating-an-offer-via-the-wizard.md#delivering-with-a-call-to-the-offer-engine)を参照してください。

1. 変更を保存します。
1. **[!UICONTROL メール配信]**&#x200B;アクティビティを右クリックして開きます。
1. 母集団とトラッキングログを取得するために、「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションを選択します。

   ![](assets/wkf_cross-channel_2.png)

   この情報を使用して、最初のメールを受信したときの受信者の行動に基づいて別の配信を送信することができます。

1. 受信者がメールを開封するのを数日待つための&#x200B;**[!UICONTROL 待機]**&#x200B;アクティビティを追加します。

   ![](assets/wkf_cross-channel_4.png)

## 手順 3：得られたオーディエンスのセグメント化 {#step-3--segmenting-the-resulting-audience}

ターゲットを特定し、最初の配信を作成した後は、フィルター条件を使用してターゲットを別々の母集団にセグメント化する必要があります。

1. **分割**&#x200B;アクティビティをワークフローに追加し、開きます。このアクティビティの使用について詳しくは、[この節](split.md)を参照してください。
1. クエリでアップストリームを計算した母集団から 3 つのセグメントを作成します。

   ![](assets/wkf_cross-channel_6.png)

1. 1 番目のサブセットでは、「**[!UICONTROL インバウンド母集団に対するフィルター条件を追加]**」オプションを選択し、「**[!UICONTROL 編集]**」をクリックします。

   ![](assets/wkf_cross-channel_8.png)

1. 制限フィルターとして「**[!UICONTROL 配信の受信者]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/wkf_cross-channel_9.png)

1. フィルター設定で、「**[!UICONTROL 行動]**」ドロップダウンリストから「**[!UICONTROL (メールを) 開封またはクリックしなかった受信者]**」を選択し、送信するオファーを含んだメールを配信リストから選択します。「**[!UICONTROL 終了]**」をクリックします。

   ![](assets/wkf_cross-channel_10.png)

1. 2 番目のサブセットでも同様に、「**[!UICONTROL 行動]**」ドロップダウンリストから「**[!UICONTROL （メールを）クリックしていない受信者]**」を選択します。

   ![](assets/wkf_cross-channel_11.png)

1. 3 番目のサブセットでは、「**[!UICONTROL インバウンド母集団に対するフィルター条件を追加]**」を選択し、「**[!UICONTROL 編集]**」をクリックして、「**[!UICONTROL 特定のフィルタリングディメンションを使用]**」オプションを選択します。
1. 「**[!UICONTROL フィルタリングディメンション]**」ドロップダウンリストから「**[!UICONTROL 受信者トラッキングログ]**」を選択し、「**[!UICONTROL 制限フィルターのリスト]**」から「**[!UICONTROL フィルター条件]**」をハイライトして、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/wkf_cross-channel_12.png)

1. 次のようにフィルター条件を選択します。

   ![](assets/wkf_cross-channel_13.png)

1. 「**[!UICONTROL 完了]**」をクリックして変更を保存します。

## 手順 4：ワークフローの最終処理 {#step-4--finalizing-the-workflow}

1. **[!UICONTROL 分割]**&#x200B;アクティビティから 3 つのサブセットを生成した後、次のように関連アクティビティをワークフローに追加します。

   * **[!UICONTROL 1 番目のサブセットにリマインダーのメールを送信するメール配信]**&#x200B;アクティビティを追加します。
   * 2 番目のサブセットに SMS メッセージを送信する&#x200B;**[!UICONTROL モバイル配信]**&#x200B;アクティビティを追加します。
   * 対応する受信者をデータベースに追加する&#x200B;**[!UICONTROL リスト更新]**&#x200B;アクティビティを追加します。

1. ワークフローの配信アクティビティをダブルクリックして編集します。メールおよび SMS の作成について詳しくは、[メールチャネル](../../delivery/using/about-email-channel.md)および [SMS チャネル](../../delivery/using/sms-channel.md)を参照してください。
1. **[!UICONTROL リスト更新]**&#x200B;アクティビティをダブルクリックし、「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションを選択します。

   これで、得られた受信者を Adobe Campaign から Adobe Experience Cloud にエクスポートすることができます。例えば、**[!UICONTROL 共有オーディエンスを更新]**&#x200B;アクティビティをワークフローに追加することで、Adobe Target でそのオーディエンスを使用することができます．詳しくは、[オーディエンスのエクスポート](../../integrations/using/importing-and-exporting-audiences.md#exporting-an-audience)を参照してください。

1. アクションバーの「**開始**」ボタンをクリックして、ワークフローを実行します。

**クエリ**&#x200B;アクティビティでターゲティングされた母集団はセグメント化され、受信者の行動に基づいて、メール配信か SMS 配信を受信します。残りの母集団は、**[!UICONTROL リスト更新]**&#x200B;アクティビティを使用して、データベースに追加されます。
