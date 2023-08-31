---
product: campaign
title: PI の閲覧を制限
description: PI の閲覧を制限する方法を学ぶ
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: PI
role: Data Engineer, Developer
exl-id: 0f32d62d-a10a-4feb-99fe-4679b98957d4
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 71%

---

# PI の閲覧を制限{#restricting-pii-view}

## 概要 {#overview}

データレコードにアクセスするためにマーケティングユーザーが必要で、名、姓、電子メールアドレスなどの個人識別情報 (PII) を表示したくないお客様もいます。 Adobe Campaign は、プライバシーを保護し、一般のキャンペーンオペレーターによるデータの乱用を防止するための方法を提案します。

## 実装 {#implementation}

任意の要素または属性に適用できる新しい属性がスキーマに追加され、既存の属性を補完します。 **[!UICONTROL visibleIf]** . この属性は **[!UICONTROL accessibleIf]** です。 現在のユーザーコンテキストに関連する XTK 式を含む場合、例えば **[!UICONTROL HasNamedRight]** や **[!UICONTROL $(login)]** を利用できます。

この使用法を示す受信者スキーマ拡張のサンプルを以下に示します。

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

* **[!UICONTROL visibleIf]**：メタデータからフィールドが非表示になります。したがって、スキーマ表示、列選択、式ビルダー内でフィールドにアクセスすることはできません。 ただし、フィールド名を式に手動で入力した場合は、値が表示され、データは非表示にはなりません。
* **[!UICONTROL accessibleIf]**：結果のクエリからデータを非表示にします（空の値に置き換えます）。 visibleIf が空の場合は、次と同じ式を取得します。 **[!UICONTROL accessibleIf]** .

Campaign でこの属性を使用した場合の結果は次のとおりです。

* コンソールの汎用クエリエディターを使用してデータを表示することはありません。
* 概要リストとレコードリスト（コンソール）にはデータが表示されません。
* 詳細表示では、データは読み取り専用になります。
* データは、フィルター内でのみ使用できます（つまり、二分法を使用して値を推測することは可能です）。
* 制限付きフィールドを使用して作成された式も制限されます。lower（@email）は @email と同様にアクセス可能になります。
* ワークフローでは、制限付きの列をトランジションの追加の列としてターゲット母集団に追加できますが、Adobe Campaign ユーザーはアクセスできません。
* ターゲット母集団をグループ（リスト）に保存する場合、保存されるフィールドの特性はデータのソースと同じです。
* デフォルトでは、JS コードからデータにアクセスできません。

## 推奨事項 {#recommendations}

各配信で、E メールアドレスは **[!UICONTROL broadLog]** そして **[!UICONTROL forecastLog]** テーブル：結果として、これらのフィールドも保護する必要があります。

以下に、これを実装するログテーブル拡張のサンプルを示します。

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
>この制限は、技術以外のユーザーに適用されます。関連する権限を持つ技術ユーザーは、データを取得できます。 したがって、この方法は 100%安全ではありません。
