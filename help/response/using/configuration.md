---
product: campaign
title: Campaign Response Manager の設定
description: Campaign Response Manager の設定方法を説明します
feature: Campaigns
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: campaign
content-type: reference
topic-tags: response-manager
exl-id: 1a115ca9-2532-4bd3-be77-814e43250c51
TQID: https://experienceleague.adobe.com/P89PBe23uuRmGX5vb6lCNd8kTd24peaZcKsTRAj2pnw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 796
ht-degree: 66%

---

# Campaign Response Manager の設定{#configuration}



この節は反応管理の設定担当者向けです。 スキーマの拡張、ワークフローの定義および SQL プログラミングについて、ある程度の知識があることを前提としています。

個人のテーブルを使用して、標準データモデルを Adobe Campaign 外のトランザクションテーブルの特定の特性に合わせて調整する方法を説明します。 この個人のテーブルは、Adobe Campaign 内の使用可能な個人のテーブルや他のテーブルと一致する場合があります。

測定の仮説は、オペレーションプロセスワークフロー（**[!UICONTROL operationMgt]**）により開始します。 各仮説は、実行ステータス（「編集中」、「保留中」、「完了」、「失敗」など）と非同期的に実行される個別のプロセスを表します。 優先度の制約、同時プロセス数の制限、ローアクティビティページ、頻度を持つ自動実行を管理するスケジューラーによって制御されます。

## スキーマの設定 {#configuring-schemas}

>[!CAUTION]
>
>アプリケーションのビルトインのスキーマは変更しないでください。その代わりに、スキーマ拡張メカニズムを使用します。 標準スキーマを変更すると、今後アプリケーションのアップグレード時にスキーマが更新されなくなり、 Adobe Campaign の使用中に誤作動が生じる可能性があります。

測定する様々なテーブル（トランザクション、トランザクションの詳細）に加え、テーブルと配信、オファーおよび個人間の関係を定義するには、反応モジュールを使用する前にアプリケーションを統合する必要があります。

### 標準スキーマ {#standard-schemas}

標準の&#x200B;**[!UICONTROL nms:remaMatch]** スキーマには、反応ログテーブル（個人、仮説、トランザクションテーブル間の関係）が含まれています。 このスキーマは、反応ログの最終的な宛先テーブルの継承済みスキーマとして使用します。

**[!UICONTROL nms:remaMatchRcp]** スキーマも標準として提供され、Adobe Campaign受信者（**[!UICONTROL nms:recipient]**）のリアクションログのストレージが含まれています。 このスキーマを使用するには、拡張してトランザクションテーブル（購入などを含む）にマップする必要があります。

### トランザクションテーブルとトランザクションの詳細 {#transaction-tables-and-transaction-details}

トランザクションテーブルには、個人への直接リンクを含める必要があります。

必要に応じて、トランザクションの詳細を含むテーブルを追加することもできます。 このテーブルは個人に直接リンクしません。

領収書を例にすると、トランザクションテーブルはコンタクト先（領収書テーブル）にリンクし、領収書ラインテーブルは領収書テーブル（詳細テーブル）にのみリンクします。 この後、領収書ラインテーブルが領収書テーブルにリンクされているレベルで、仮説を直接設定できます。

>[!NOTE]
>
>仮説で想定される動作を説明する受領者識別子を保持する場合は、nms:remaMatchRcp テーブルテンプレートを拡張して識別子を追加できます（この場合、これらのフィールドにROI計算はリンクされません）。

イベントの日付を追加することを強くお勧めします。

以下のスキーマは、設定完了後の複数テーブル間の結合を表します。

![](assets/response_data_model.png)

### 応答管理と受信者 {#response-management-with-adobe-campaign-recipients}

この例では、Adobe Campaignの組み込み受信者テーブル **[!UICONTROL nms:recipient]**&#x200B;を使用して、応答管理モジュールに購入表を統合します。

**[!UICONTROL nms:remaMatchRcp]**&#x200B;受信者の応答ログのテーブルが拡張され、購入テーブルスキーマへのリンクが追加されます。 次の例では、購入テーブルの名前は&#x200B;**demo:purchase**&#x200B;です。

1. Adobe Campaign エクスプローラーで、**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL ターゲットマッピング]**&#x200B;を選択します。
1. **受信者**&#x200B;を右クリックし、**[!UICONTROL アクション]**／**[!UICONTROL ターゲティングディメンションのオプションを変更]**&#x200B;を選択します。

   ![](assets/delivery_mapping1.png)

1. 次のウィンドウで「**[!UICONTROL 拡張名前空間]**」をパーソナライズできます。パーソナライズしたら、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/delivery_mapping2.png)

1. 「**[!UICONTROL 反応管理]**」カテゴリで、「**[!UICONTROL 反応のストレージスキーマを生成]**」ボックスがオンになっていることを確認します。

   次に、**[!UICONTROL 追加フィールドを定義…]**&#x200B;をクリックして、関連するトランザクションテーブルを選択し、目的のフィールドをnms:remaMatchRcp スキーマの拡張機能に追加します。

   ![](assets/delivery_mapping3.png)

作成したスキーマは以下のようになります。

```
<srcSchema _cs="Reactions (Recipients) (cus)" entitySchema="xtk:srcSchema" extendedSchema="nms:remaMatchRcp" 
img="nms:remaMatch.png" implements="xtk:persist" label="Reactions (Recipients)" mappingType="sql"
name="remaMatchRcp" namespace="cus">  
 <element label="Reactions (Recipients)" name="remaMatchRcp">    
  <key internal="true" name="match">      
   <keyfield xlink="hypothesis"/>      
   <keyfield xlink="broadLog"/>      
   <keyfield xlink="proposition"/>    
  </key>    
  <attribute label="Quantity" name="quantity" type="long"/>    
  <element name="purchase" target="demo:purchase" type="link"/>    
  <element name="hypothesis" revLabel="Reactions (Recipients)" revLink="remaMatchRcp"/>    
  <element applicableIf="HasPackage('nms:coreInteraction')" label="Proposition" name="proposition" target="nms:propositionRcp" type="link"/>   
  <element desc="Message (Delivery log)" label="Message" name="broadLog" target="nms:broadLogRcp" type="link"/>    
  <element label="Respondent" name="responder" target="nms:recipient" type="link"/>  
 </element>  
 <createdBy _cs="Administrator (admin)"/>  
 <modifiedBy _cs="Administrator (admin)"/>
</srcSchema>
```

### パーソナライズした受信者テーブルを使用した応答管理 {#response-management-with-a-personalized-recipient-table}

この例では、Adobe Campaign で使用可能な受信者テーブル以外の個人のテーブルを使用して、購入テーブルを応答管理モジュールに統合します。

* **[!UICONTROL nms:remaMatch]** スキーマから派生した新しい応答ログスキーマを作成します。

  個人のテーブルはAdobe Campaign受信者のテーブルとは異なるため、**[!UICONTROL nms:remaMatch]** スキーマに基づいて応答ログの新しいスキーマを作成する必要があります。 このスキーマに配信ログと購入テーブルへのリンクを入力します。

  次の例では、**demo:broadLogPers** スキーマと&#x200B;**demo:purchase** トランザクションテーブルを使用します。

  ```
  <srcSchema desc="Linking of a recipient transaction to a hypothesis"    
  img="nms:remaMatch.png" label="Responses on persons" labelSingular="Responses on a person" name="remaMatchPers" namespace="nms">
    <element name="remaMatchPers" template="nms:remaMatch">
      <key internal="true" name="match">
        <keyfield xlink="hypothesis"/>
       <keyfield xlink="purchase"/>
      </key>
  
      <element name="hypothesis" revLabel="Response logs for persons" revLink="remaMatchPers"/>
      <element applicableIf="HasPackage('nms:interaction')" label="Proposition" name="proposition"
               target="demo:propositionPers" type="link"/>
      <element label="Delivery log" name="broadLog" target="demo:broadLogPers" type="link"/>
    </element>
  </srcSchema>
  ```

* **[!UICONTROL nms:remaHypothesis]** スキーマの仮説フォームを変更します。

  デフォルトでは、反応ログのリストは受信者ログに表示されます。 上述の手順で作成した新しい反応ログを表示するには、仮説フォームを修正する必要があります。

  次に例を示します。

  ```
   <container type="visibleGroup" visibleIf="[context/@remaMatchStorage]= 'demo:remaMatchPers'">
                <input hideEditButtons="true" img="nms:remaMatch.png" nolabel="true" refresh="true"
                 toolbarCaption="Responses generated by the hypothesis" type="linklist"
                 xpath="remaMatchPers">
            <input xpath="[.]"/>
            <input xpath="@controlGroup"/>
          </input>
     </container> 
  ```

## 指標の管理 {#managing-indicators}

Response Manager モジュールには、事前定義済みの指標のリストが用意されていますが、 この他にパーソナライズした測定指標を追加することもできます。

追加するには、新しい指標それぞれに 2 つのフィールドを挿入して仮説テーブルを拡張する必要があります。

* 1 つ目のフィールドはターゲット母集団用、
* 2 つ目はコントロール母集団用です。

例：

```
<srcSchema entitySchema="xtk:srcSchema" extendedSchema="nms:remaHypothesis" label="Measurement hypothesis" 
md5="1D4DED54FF8EC2432AED6736EDE6F547" name="remaHypothesis" namespace="demo" xtkschema="xtk:srcSchema">  
    <element name="remaHypothesis">    
        <element name="indicators">      
            <!-- Quantity -->      
            <attribute label="Total contacted" name="contactReactedTotalQuantity" type="long"/>
            <attribute label="Total number of people in the control group" name="proofReactedTotalquantity" type="long"/> 
        </element> 
    </element>
</srcSchema>
```
