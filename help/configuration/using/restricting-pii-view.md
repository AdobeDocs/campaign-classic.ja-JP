---
title: PII 表示の制限
seo-title: PII 表示の制限
description: PII 表示の制限
seo-description: null
page-status-flag: never-activated
uuid: 4dddc7f5-dac3-47b3-b3cb-92b47eb595fa
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 550439c1-978c-414e-be5b-a9e1a202c4cd
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 8%

---


# PII 表示の制限{#restricting-pii-view}

## 概要 {#overview}

一部の顧客は、マーケティングユーザーがデータレコードにアクセスできることを必要としているが、名、姓、電子メールアドレスなど、個人識別情報(PII)を表示してほしくないと考えています。 Adobe Campaign は、プライバシーを保護し、一般のキャンペーンオペレーターによるデータの乱用を防止するための方法を提案します。

## 実装 {#implementation}

任意のスキーマまたは属性に適用できる新しい属性が要素に追加され、既存の属性 **[!UICONTROL visibleIfを補完します]** 。 この属性は次のとおりです。 **[!UICONTROL accessibleIf]** . 現在のユーザコンテキストに関連するXTK式を含む場合、 **[!UICONTROL HasNamedRight]** や **[!UICONTROL $(login)]** などを利用できます。

以下に受信者スキーマ拡張の例を示します。

```
<srcSchema desc="Recipient table (profiles" entitySchema="xtk:srcSchema" extendedSchema="nms:recipient"
           img="nms:recipient.png" label="Recipients" labelSingular="Recipient"
           name="recipient" namespace="sec" xtkschema="xtk:srcSchema">
  <element desc="Recipient table (profiles" img="nms:recipient.png" label="Recipients"
           labelSingular="Recipient" name="recipient">
    <attribute name="firstName" accessibleIf="$(login)=='admin'"/>
    <attribute name="lastName" visibleIf="$(login)=='admin'"/>
    <attribute name="email" accessibleIf="$(login)=='admin'"/>
  </element>
</srcSchema>
```

主なプロパティは次のとおりです。

* **[!UICONTROL visibleIf]** :を指定すると、メタデータからフィールドが非表示になります。したがって、スキーマ表示、列選択、式ビルダー内でフィールドにアクセスすることはできません。 ただし、式にフィールド名を手動で入力した場合は、値が表示され、データは非表示にはなりません。
* **[!UICONTROL accessibleIf]** :結果のクエリからデータを非表示にします（空の値に置き換えます）。 visibleIfが空の場合、 **[!UICONTROL accessibleIfと同じ式を取得します]** 。

キャンペーンでこの属性を使用した場合の結果は次のとおりです。

* コンソールの汎用クエリエディターを使用してデータを表示しない。
* 概要リストとレコードリスト（コンソール）にはデータが表示されません。
* 詳細表示では、データは読み取り専用になります。
* データは、フィルター内でのみ使用できます（つまり、いくつかのディコトモーション法を使用して、引き続き値を推測できます）。
* 制限付きフィールドを使用して作成された式は、次の条件に従って制限されます。lower(@email)は、@emailと同様にアクセス可能になります。
* ワークフローでは、ターゲット母集団に制限付きの列をトランジションの追加の列として追加できますが、Adobe Campaignユーザーはアクセスできません。
* ターゲット母集団をグループ(リスト)に格納する場合、格納されるフィールドの特性は、データのソースと同じです。
* デフォルトでは、JSコードからデータにアクセスできません。

## 推奨事項 {#recommendations}

各配信で、電子メールアドレスが **[!UICONTROL broadLog]** 表と **[!UICONTROL forecastLog]** 表にコピーされます。そのため、これらのフィールドも保護する必要があります。

以下に、これを実装するログテーブル拡張の例を示します。

```
<srcSchema entitySchema="xtk:srcSchema" extendedSchema="nms:broadLogRcp" img="nms:broadLog.png"
           label="Recipient delivery logs" labelSingular="Recipient delivery log"
           name="broadLogRcp" namespace="sec" xtkschema="xtk:srcSchema">
  <element img="nms:broadLog.png" label="Recipient delivery logs" labelSingular="Recipient delivery log"
           name="broadLogRcp">
    <attribute accessibleIf="$(login)=='admin'" name="address"/>
  </element>
</srcSchema>
<srcSchema desc="Delivery messages being prepared." entitySchema="xtk:srcSchema"
           extendedSchema="nms:tmpBroadcast" img="" label="Messages being prepared"
           labelSingular="Message" name="tmpBroadcast" namespace="sec" xtkschema="xtk:srcSchema">
  <element desc="Delivery messages being prepared." label="Messages being prepared"
           labelSingular="Message" name="tmpBroadcast">
    <attribute accessibleIf="$(login)=='admin'" name="address"/>
  </element>
</srcSchema>
<srcSchema entitySchema="xtk:srcSchema" extendedSchema="nms:excludeLogRcp" img="nms:excludeLog.png"
           label="Recipient exclusion logs" labelSingular="Recipient exclusion log"
           name="excludeLogRcp" namespace="sec" xtkschema="xtk:srcSchema">
  <element img="nms:excludeLog.png" label="Recipient exclusion logs" labelSingular="Recipient exclusion log"
           name="excludeLogRcp">
    <attribute accessibleIf="$(login)=='admin'" name="address"/>
  </element>
</srcSchema>
```

>[!NOTE]
>
>この制限は、技術者以外のユーザーに適用されます。関連する権限を持つ技術ユーザーは、データを取得できます。 したがって、この方法は100%のセキュリティで保護されません。

