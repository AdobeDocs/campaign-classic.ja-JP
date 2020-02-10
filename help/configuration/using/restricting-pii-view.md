---
title: PIIビューの制限
seo-title: PIIビューの制限
description: PIIビューの制限
seo-description: null
page-status-flag: never-activated
uuid: 4dddc7f5-dac3-47b3-b3cb-92b47eb595fa
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 550439c1-978c-414e-be5b-a9e1a202c4cd
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# PIIビューの制限{#restricting-pii-view}

## 概要 {#overview}

一部の顧客は、マーケティングユーザーがデータレコードにアクセスできるようにする必要があるが、名、姓、電子メールアドレスなどの個人識別情報(PII)を表示しないようにします。 Adobe Campaign は、プライバシーを保護し、一般のキャンペーンオペレーターによるデータの乱用を防止するための方法を提案します。

## 実装 {#implementation}

任意の要素または属性に適用できる新しい属性がスキーマに追加され、既存の属性が補完されます **[!UICONTROL visibleIf]** 。 この属性は次のとおりです。 **[!UICONTROL accessibleIf]** . 現在のユーザーコンテキストに関連するXTK式を含む場合、例えば、またはを **[!UICONTROL HasNamedRight]** 使用す **[!UICONTROL $(login)]** ることができます。

以下に、この使用法を示す受信者スキーマ拡張の例を示します。

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

* **[!UICONTROL visibleIf]** :メタデータからフィールドを非表示にします。したがって、スキーマビュー、列選択、または式ビルダー内でフィールドにアクセスすることはできません。 ただし、式にフィールド名を手動で入力した場合は、値が表示されるので、データは非表示にはなりません。
* **[!UICONTROL accessibleIf]** :結果のクエリからデータを非表示にします（空の値に置き換えます）。 visibleIfが空の場合、と同じ式を取得します **[!UICONTROL accessibleIf]** 。

Campaignでこの属性を使用すると、次のような結果が生じます。

* コンソールの汎用クエリエディターを使用してデータを表示しない。
* 概要リストとレコードリスト（コンソール）にはデータが表示されません。
* 詳細ビューでは、データは読み取り専用になります。
* データは、フィルター内でのみ使用できます（つまり、ディコトミーの戦略を使用しても、引き続き値を推測できます）。
* 制限付きフィールドを使用して作成された式は、次のように制限されます。lower(@email)は、@emailと同様にアクセス可能になります。
* ワークフローでは、制限付きの列をターゲット訪問者にトランジションの追加の列として追加できますが、Adobe Campaignユーザーはアクセスできません。
* ターゲット母集団をグループ（リスト）に格納する場合、格納されるフィールドの特性はデータのソースと同じです。
* デフォルトでは、JSコードからデータにアクセスできません。

## 推奨事項 {#recommendations}

各配信で、電子メールアドレスが表と表にコ **[!UICONTROL broadLog]** ピーされ **[!UICONTROL forecastLog]** ます。その結果、これらのフィールドも保護する必要があります。

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
>この制限は、技術者以外のユーザーに適用されます。関連する権限を持つ技術ユーザーは、データを取得できます。 したがって、この方法は100%のセキュリティで保護されていません。

