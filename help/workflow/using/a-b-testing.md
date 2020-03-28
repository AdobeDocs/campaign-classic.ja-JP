---
title: A/B テスト
seo-title: A/B テスト
description: A/B テスト
seo-description: null
page-status-flag: never-activated
uuid: 8887574e-447b-48a5-afc6-95783ffa7fb3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: use-cases
discoiquuid: 4113c3fe-a279-4fe1-be89-ea43c96edc34
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# A/B テスト{#a-b-testing}

E メール配信の複数のコンテンツがあり、どのバージョンがターゲットの母集団に対し効果的なコンテンツであるのかを見極めたい場合、一部の受信者に対し異なるバージョンを送信してその中から最も成功率の高かったものを選び出し、それを残りの受信者に送信するといったことが可能です。

この使用例では、ターゲティングワークフローを使用して、2 つの E メール配信コンテンツを比較します。どちらの配信でも、メッセージとテキストは同一とし、レイアウトのみを変更します。

ターゲットの母集団は 3 つに分割します。2 つのテストグループと、その他の母集団です。各テストグループに別々のバージョンを配信します。配信完了から 5 日間の待機期間を設定します。この待機期間の終了後に結果を集め、開封率の最も高いものを見極めます。次に、最もスコアの高い配信コンテンツをスクリプトで復元し、テストグループとして使用しなかった母集団に送信します。

どの配信で最もスコアが高いのかを判断する基準は、個々のニーズに応じて変わる可能性がある点に注意してください。開封率、クリックスルー率、購読率、応答度などが、この判断基準の候補として挙げられます。

また、この使用例で説明したテストでは 2 つの配信だけしか扱っていませんが、必要に応じてもっと多くのバージョンをテストすることもできます。その場合は、単にアクティビティをワークフローに追加するだけです。

A/B テストを作成するには、次の手順に従います

* [手順 1：ターゲティングワークフローの作成](#step-1--creating-a-targeting-workflow)
* [手順 2：母集団サンプルの設定](#step-2--configuring-population-samples)
* [手順 3：2 つの配信テンプレートの作成](#step-3--creating-two-delivery-templates)
* [手順 4：ワークフローでの配信の設定](#step-4--configuring-the-deliveries-in-the-workflow)
* [手順 5：スクリプトの作成](#step-5--creating-the-script)
* [手順 7：ワークフローの開始](#step-7--starting-the-workflow)
* [手順 8：結果の分析](#step-8--analyzing-the-result)

## 手順 1：ターゲティングワークフローの作成 {#step-1--creating-a-targeting-workflow}

キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブでワークフローを作成する必要があります。このワークフローは、1 つの「**[!UICONTROL クエリ]**」アクティビティ、2 つの「**[!UICONTROL E メール配信]**」アクティビティとリンクした 1 つの「**[!UICONTROL 分割]**」アクティビティ、1 つの「**[!UICONTROL 待機]**」アクティビティ、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ、1 つの「**[!UICONTROL 配信]**」アクティビティから構成されます。

1. まだ作成していない場合は、キャンペーンを作成します（詳細は、この[節](../../campaign/using/setting-up-marketing-campaigns.md#creating-a-campaign)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_001.png)

1. 「**[!UICONTROL ターゲティングとワークフロー]**」タブに移動します。

   ![](assets/use_case_abtesting_targetwkfl_002.png)

1. 既存のワークフローのラベルを変更するか、「**[!UICONTROL 追加]**」をクリックして、新しいラベルを作成します（これについて詳細は、この[節](../../campaign/using/marketing-campaign-deliveries.md#selecting-the-target-population)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_003.png)

1. マウスを使用してワークフローダイアグラムにアクティビティをドラッグ＆ドロップします。対象となるアクティビティには、1 つの「**[!UICONTROL クエリ]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、1 つの「**[!UICONTROL 分割]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、2 つの「**[!UICONTROL E メール配信]**」アクティビティ（「**[!UICONTROL 配信]**」タブ）、1 つの「**[!UICONTROL 待機]**」アクティビティ（「**[!UICONTROL フロー制御]**」タブ）、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）、1 つの「**[!UICONTROL 配信]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）などがあります。

![](assets/use_case_abtesting_targetwkfl_004.png)

## 手順 2：母集団サンプルの設定 {#step-2--configuring-population-samples}

### 「クエリ」アクティビティの設定{#configuring-the-query-activity}

* 「**[!UICONTROL クエリ]**」アクティビティをダブルクリックします。

   ![](assets/use_case_abtesting_createrecipients_001.png)

* 「**[!UICONTROL クエリを編集]**」リンクをクリックし、ターゲティング対象の受信者を選択します。

   ![](assets/use_case_abtesting_createrecipients_002.png)

* 「**[!UICONTROL クエリ]**」アクティビティを「**[!UICONTROL 分割]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createrecipients_003.png)

### 分割アクティビティの設定 {#configuring-the-split-activity}

このアクティビティでは、配信 A を受信する母集団、配信 B を受信する母集団、その他の母集団といったように複数の母集団を作成することができます。ランダムな抽出をおこなうことで、各配信の母集団の部分のみをターゲティングすることが可能です。

1. 母集団 A の作成

   * 「**[!UICONTROL 分割]**」アクティビティをダブルクリックします。

      ![](assets/use_case_abtesting_createrecipients_004.png)

   * 既存のタブで、ラベルを母集団 A に変更します。

      ![](assets/use_case_abtesting_createrecipients_005.png)

   * 「**[!UICONTROL 選択レコード数の制限]**」オプションを選択します。

      ![](assets/use_case_abtesting_createrecipients_006.png)

   * 「**[!UICONTROL 編集]**」リンクをクリックし、「**[!UICONTROL ランダムサンプリングを有効化]**」を選択して、「**[!UICONTROL 次へ]**」をクリックします。

      ![](assets/use_case_abtesting_createrecipients_007.png)

   * しきい値を 10% に設定して、「**[!UICONTROL 完了]**」をクリックします。

      ![](assets/use_case_abtesting_createrecipients_008.png)

1. 母集団 B の作成

   * 「**[!UICONTROL 追加]**」をクリックして、母集団 B に使用する新しいタブを作成します。

      ![](assets/use_case_abtesting_createrecipients_009.png)

   * A と同じように、母集団を 10% に制限します。

      ![](assets/use_case_abtesting_createrecipients_010.png)

1. その他の母集団の作成

   * 「**[!UICONTROL 一般]**」タブに移動します。

      ![](assets/use_case_abtesting_createrecipients_011.png)

   * 「**[!UICONTROL 補集合を生成]**」を選択します。

      ![](assets/use_case_abtesting_createrecipients_012.png)

   * ラベルを変更して、この母集団には A も B も含まれないように指定し、「**[!UICONTROL OK]**」をクリックしてアクティビティを閉じます。

      ![](assets/use_case_abtesting_createrecipients_013.png)

## 手順 3：2 つの配信テンプレートの作成 {#step-3--creating-two-delivery-templates}

ここでは、2 つの配信テンプレートを作成します。各テンプレートは、「**[!UICONTROL 分割]**」アクティビティとリンクした「**[!UICONTROL E メール配信]**」アクティビティで参照されます。詳しくは、[この節](../../delivery/using/about-templates.md)を参照してください。

1. **[!UICONTROL リソース／配信テンプレート]**&#x200B;フォルダーへ移動します。
1. 「**[!UICONTROL E メール]**」配信テンプレートを複製します。

   ![](assets/use_case_abtesting_deliverymodel_001.png)

1. 配信 A に使用するコンテンツを作成します。

   ![](assets/use_case_abtesting_deliverymodel_002.png)

1. この手順を繰り返し、配信 B のテンプレートも作成します。

   ![](assets/use_case_abtesting_deliverymodel_003.png)

## 手順 4：ワークフローでの配信の設定 {#step-4--configuring-the-deliveries-in-the-workflow}

次のステップで配信を設定します。設定する配信は、前のステージの[手順 2：母集団サンプルの設定](#step-2--configuring-population-samples)で作成した 3 つの母集団用のものです。最初の 2 つの配信では、母集団 A と母集団 B にそれぞれ異なるコンテンツを送信することができます。一方、3 番目の配信は、A の配信も B の配信も受信しない母集団用のものです。このコンテンツはスクリプトで割り出します。A のコンテンツと B のコンテンツのどちらかと同一のものになり、どちらのコンテンツの開封率が高いかに応じて決まります。3 番目の配信の待機期間を設定し、配信 A、配信 B の結果を特定する必要があります。そのため、3 番目の配信には「**[!UICONTROL 待機]**」アクティビティを実装します。

1. 「**[!UICONTROL 分割]**」アクティビティに移動し、母集団 A 用のトランジションを、既にワークフローにある E メール配信のトランジションとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_001.png)

1. 配信をダブルクリックして開きます。
1. ドロップダウンリストで、配信 A のテンプレートを選択します。

   ![](assets/use_case_abtesting_createdeliveries_003.png)

1. 「**[!UICONTROL 続行]**」をクリックして配信を表示し、保存します。

   ![](assets/use_case_abtesting_createdeliveries_002.png)

1. 母集団 B 用の「**[!UICONTROL 分割]**」アクティビティのトランジションを 2 番目の E メール配信にリンクします。

   ![](assets/use_case_abtesting_createdeliveries_004.png)

1. 配信を開き、配信 B のテンプレートを選択し、配信を保存します。

   ![](assets/use_case_abtesting_createdeliveries_005.png)

1. その他の母集団用のトランジションを「**[!UICONTROL 待機]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_006.png)

1. **[!UICONTROL 待機]**&#x200B;アクティビティを開き、5 日の待機期間を設定します。

   ![](assets/use_case_abtesting_createdeliveries_007.png)

1. 「**[!UICONTROL 待機]**」アクティビティを「**[!UICONTROL JavaScript コード]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_008.png)

## 手順 5：スクリプトの作成 {#step-5--creating-the-script}

その他の母集団用の配信コンテンツを、スクリプトで割り出します。このスクリプトでは、最も開封率の高い配信について情報を復元し、その内容を最終の配信にコピーします。

### スクリプトの例 {#example-of-a-script}

ターゲティングワークフローで、以下のようにスクリプトを使用します。詳しくは、[実装](#implementation)を参照してください。

```
 // query the database to find the winner (best open rate)
   var winner = xtk.queryDef.create(
     <queryDef schema="nms:delivery" operation="get">
       <select>
         <node expr="@id"/>
         <node expr="@label"/>
         <node expr="[@operation-id]"/>
         <node expr="[@workflow-id]"/>
       </select>
       <where>
         <condition expr={"@FCP=0 and [@workflow-id]= " + instance.id}/>
       </where>
       <orderBy>
         <node expr="[indicators/@estimatedRecipientOpenRatio]" sortDesc="true"/>
       </orderBy>
     </queryDef>).ExecuteQuery()
   
   // create a new delivery object and initialize it by doing a copy of
   // the winner delivery
   var delivery = nms.delivery.create()
   delivery.Duplicate("nms:delivery|" + winner.@id)

   // append 'final' to the delivery label
   delivery.label = winner.@label + " final"

   // link the delivery to the operation to make sure it will be displayed in
   // the campaign dashboard. This attribute needs to be set manually here since 
   // the Duplicate() method has reset it to its default value => 0
   delivery.operation_id = winner.@["operation-id"]
   delivery.workflow_id = winner.@["workflow-id"]

   // adjust some delivery parameters to make it compatible with the 
   // "Prepare and start" option selected in the Delivery tab of this activity
   delivery.scheduling.validationMode = "manual"
   delivery.scheduling.delayed = 0
 
   // save the delivery in database
   delivery.save()
 
   // store the new delivery Id in event variables
   vars.deliveryId = delivery.id
```

スクリプトについて詳しくは、[スクリプトの詳細](#details-of-the-script)を参照してください。

### 実装 {#implementation}

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを開きます。
1. [スクリプトの例](#example-of-a-script)で提供されたスクリプトを **[!UICONTROL JavaScript コード]**&#x200B;ウィンドウにコピーします。

   ![](assets/use_case_abtesting_configscript_002.png)

1. 「**[!UICONTROL ラベル]**」フィールドに、次のようなスクリプト名を入力します。

   ```
   <%= vars.deliveryId %>
   ```

   ![](assets/use_case_abtesting_configscript_003.png)

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを閉じます。
1. ワークフローの保存

### スクリプトの詳細 {#details-of-the-script}

このセクションでは、スクリプトの様々な機能とその動作モードについて詳しく説明します。

* まずはじめは、クエリです。**queryDef** コマンドでは、ターゲティングワークフローを実行して作成した配信を「**NmsDelivery**」テーブルから復元することや、それらの配信を推定の開封率に応じて並べ替えることでき、開封率の高い配信の情報が復元されます。

   ```
   // query the database to find the winner (best open rate)
      var winner = xtk.queryDef.create(
        <queryDef schema="nms:delivery" operation="get">
          <select>
            <node expr="@id"/>
            <node expr="@label"/>
            <node expr="[@operation-id]"/>
          </select>
          <where>
            <condition expr={"@FCP=0 and [@workflow-id]= " + instance.id}/>
          </where>
          <orderBy>
            <node expr="[indicators/@estimatedRecipientOpenRatio]" sortDesc="true"/>
          </orderBy>
        </queryDef>).ExecuteQuery()
   ```

* 開封率の最も高い配信を複製します。

   ```
    // create a new delivery object and initialize it by doing a copy of
    // the winner delivery
   var delivery = nms.delivery.create()
   delivery.Duplicate("nms:delivery|" + winner.@id)
   ```

* 複製した配信のラベルを変更し、&quot;**final**&quot; という単語を追加します。

   ```
   // append 'final' to the delivery label
   delivery.label = winner.@label + " final"
   ```

* キャンペーンのダッシュボードに配信をコピーします。

   ```
   // link the delivery to the operation to make sure it will be displayed in
   // the campaign dashboard. This attribute needs to be set manually here since 
   // the Duplicate() method has reset it to its default value => 0
   delivery.operation_id = winner.@["operation-id"]
   delivery.workflow_id = winner.@["workflow-id"]
   ```

   ```
   // adjust some delivery parameters to make it compatible with the 
   // "Prepare and start" option selected in the Delivery tab of this activity
   delivery.scheduling.validationMode = "manual"
   delivery.scheduling.delayed = 0
   ```

* 配信をデータベースに保存します。

   ```
   // save the delivery in database
   delivery.save()
   ```

* 複製した配信の一意の識別子をワークフロー変数として保存します。

   ```
   // store the new delivery Id in event variables
   vars.deliveryId = delivery.id
   ```

### その他の選択基準 {#other-selection-criteria}

上記の例では、E メールの開封率に応じて配信するコンテンツを選択することができます。次のようなその他の配信固有の指標を基にすることが可能です。

* 最も高いクリックスルー率：`[indicators/@recipientClickRatio]`
* 最も高い反応率（E メールの開封やメッセージのクリック）：`[indicators/@reactivity]`
* 最も低いクレーム率：`[indicators/@refusedRatio]`（sortDesc 属性には、値 false を使用）
* 最も高いコンバージョン率：`[indicators/@transactionRatio]`
* メッセージの受信後に訪問のあったページの数：`[indicators/@totalWebPage]`
* 最も低い購読解除率：`[indicators/@optOutRatio]`
* トランザクション金額: `[indicators/@amount]`.

## 手順 6：最終配信の定義 {#step-6--defining-the-final-delivery}

A/B テストの勝者を選択するスクリプトの作成後は、最終配信のパラメーターを定義できます。

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを残りの「**[!UICONTROL 配信]**」アクティビティに接続します。
1. 「**[!UICONTROL 配信]**」アクティビティを開きます。
1. このアクティビティによってワークフローを終了するために「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションをオフにします。
1. その他のオプションはデフォルト値のままにしておきます。

   ![](assets/ab_test_final_delivery.png)

（「**[!UICONTROL Javascript コード]**」アクティビティで定義された）トランジションで指定された配信を準備することで、次の手順で説明する、承認と配信の開始が可能になります。

## 手順 7：ワークフローの開始 {#step-7--starting-the-workflow}

1. 「**[!UICONTROL 開始]**」ワークフローをクリックします。

   ![](assets/use_case_abtesting_startwkfl_001.png)

1. キャンペーンダッシュボードで、配信 A と配信 B のターゲットとコンテンツを承認します。
1. 配信を確定します。
1. 5 日間の待機が終了した後に、どのコンテンツが割り出されたのかを判断します。

   ![](assets/use_case_abtesting_startwkfl_002.png)

   このケースでは、テンプレート B が選択されます。

1. 3 番目の配信のコンテンツが決定したら、ターゲットとコンテンツを承認します。

## 手順 8：結果の分析 {#step-8--analyzing-the-result}

テストの配信が完了したら、どの受信者に配信をおこなったかをチェックし、開封の有無を確認します。

* どの受信者がターゲットになっていて、キャンペーンダッシュボードから配信を開封したのかを確認するには、「**[!UICONTROL 配信]**」タブをクリックします。

   ![](assets/use_case_abtesting_analysis_001.png)

* 配信が開封されたかどうかを確認するには、「**[!UICONTROL トラッキング]**」タブに移動します。

   ![](assets/use_case_abtesting_analysis_002.png)

* ほかの配信との比較

   ![](assets/use_case_abtesting_analysis_003.png)

この例では、配信 B の開封率が最も高くなっています。これは、コンテンツ B が最終の配信で使用されることを意味します。

![](assets/use_case_abtesting_analysis_004.png)

