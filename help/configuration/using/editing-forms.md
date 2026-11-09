---
product: campaign
title: フォームの編集
description: フォームの編集
feature: Configuration
role: Developer
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
exl-id: 24604dc9-f675-4e37-a848-f1911be84f3e
TQID: 'https://experienceleague.adobe.com/9HCx821ff3mVcpUhmpUziFpZdmAnPUC49ootzGDOjLQ'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
    internal-label: Schemas
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
    internal-label: PI
  - id: eff19c99-440a-4318-b319-444edc4d8d8f
    internal-label: Upgrade
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 758d5159759b19f7ef32e8cc8f6237547599e727
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 10%
---
# フォームの編集{#editing-forms}

## 概要

マーケターやオペレーターは、入力フォームを使用してレコードを作成、変更、プレビューできます。 Forms：データを視覚的に表現

>[!NOTE]
>
>Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 入力フォームについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms){target=_blank}を参照してください。
>
>[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms){target=_blank}

入力フォームを作成および変更できます。

* デフォルトで配信されるファクトリ入力フォームを変更できます。 工場出荷時の入力フォームは、工場のデータスキーマに基づいています。
* 定義したデータスキーマにもとづいて、カスタム入力フォームを作成できます。

Formsは`xtk:form` タイプのエンティティです。 入力フォーム構造は、`xtk:form` スキーマで表示できます。 このスキーマを表示するには、メニューから&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]**&#x200B;を選択します。 [&#x200B; フォーム構造](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms){target="_blank"}の詳細（Campaign v8 ドキュメント）を参照してください。

入力フォームにアクセスするには、メニューから&#x200B;**[!UICONTROL 管理] > [!UICONTROL 設定] > [!UICONTROL 入力フォーム]**&#x200B;を選択します。

![](assets/d_ncs_integration_form_arbo.png)

フォームをデザインするには、XML エディターでXML コンテンツを編集します。

![](assets/d_ncs_integration_form_edit.png)

[詳細情報](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#formatting){target="_blank"}（Campaign v8 ドキュメント）。

フォームをプレビューするには、「**[!UICONTROL プレビュー]**」タブをクリックします。

![](assets/d_ncs_integration_form_preview.png)

## フォームタイプ

さまざまな種類の入力フォームを作成できます。 フォームタイプは、ユーザーがフォームをどのように移動するかを決定します。

* コンソール画面

  これはデフォルトのフォームタイプです。 フォームは1 ページで構成されます。

  ![](assets/console_screen_form.png)

* コンテンツ管理

  コンテンツ管理にこのフォームタイプを使用します。 この[&#x200B; ユースケース &#x200B;](../../delivery/using/use-case-creating-content-management.md)を参照してください。

  ![](../../delivery/using/assets/d_ncs_content_form13.png)

* アシスタント

  このフォームは、特定の順序で並べられた複数のフローティングスクリーンで構成されます。 利用者は、ある画面から次の画面へ移動します。 [詳細情報](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#wizards){target="_blank"}（Campaign v8 ドキュメント）。

* アイコンボックス

  このフォームは複数のページで構成されます。 フォームを移動するには、フォームの左側にあるアイコンを選択します。

  ![](assets/iconbox_form_preview.png)

* ノートブック

  このフォームは複数のページで構成されます。 フォームを移動するには、ユーザーはフォームの上部にあるタブを選択します。

  ![](assets/notebook_form_preview.png)

* 縦長ペイン

  このフォームにはナビゲーションツリーが表示されます。

* 横長ペイン

  このフォームには、項目のリストが表示されます。

## 画像への参照

画像を検索するには、メニューから&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 構成]** > **[!UICONTROL 画像]**&#x200B;を選択します。

画像をフォーム内の要素（アイコンなど）に関連付けるには、画像への参照を追加します。 例えば、`<container>`要素で`img`属性を使用します。

構文：`img="`*`namespace`*`:`*`filename`*`.`*`extension`*`"`

次の例は、`ncm`名前空間から`book.png`および`detail.png`画像への参照を示しています。

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

これらの画像は、ユーザーがクリックして複数ページのフォームを移動するアイコンに使用されます。

![](assets/nested_forms_preview.png)


## シンプルなフォームの作成 {#create-simple-form}

フォームを作成するには、次の手順に従います。

1. メニューから、**[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**&#x200B;を選択します。
1. リストの右上にある「**[!UICONTROL 新規]**」ボタンをクリックします。

   ![](assets/input-form-create-1.png)

1. フォームプロパティを指定します。

   * フォーム名と名前空間を指定します。

     フォーム名と名前空間は、関連するデータスキーマと一致する可能性があります。  次の例は、`cus:order` データスキーマのフォームを示しています。

     ```xml
     <form entitySchema="xtk:form" img="xtk:form.png" label="Order" name="order" namespace="cus" type="iconbox" xtkschema="xtk:form">
       […]
     </form>
     ```

     または、`entity-schema`属性でデータスキーマを明示的に指定することもできます。

     ```xml
     <form entity-schema="cus:stockLine" entitySchema="xtk:form" img="xtk:form.png" label="Stock order" name="stockOrder" namespace="cus" xtkschema="xtk:form">
       […]
     </form>
     ```

   * フォームに表示するラベルを指定します。
   * 必要に応じて、フォームタイプを指定します。 フォームタイプを指定しない場合は、デフォルトでコンソール画面タイプが使用されます。

     ![](assets/input-form-create-2.png)

     マルチページフォームをデザインする場合は、`<form>`要素でフォームタイプを省略し、コンテナでタイプを指定できます。

1. 「**[!UICONTROL 保存]**」をクリックします。

1. フォーム要素を挿入します。

   例えば、入力フィールドを挿入するには、`<input>`要素を使用します。 `xpath`属性をXPath式としてフィールド参照に設定します。 [詳細情報](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/schema-structure#reference-with-xpath){target="_blank"}（Campaign v8 ドキュメント）。

   この例では、`nms:recipient` スキーマに基づく入力フィールドを示します。

   ```xml
   <input xpath="@firstName"/>
   <input xpath="@lastName"/>
   ```

1. フォームが特定のスキーマタイプに基づいている場合は、このスキーマのフィールドを検索できます。

   1. **[!UICONTROL 挿入]**/**[!UICONTROL ドキュメントフィールド]**&#x200B;をクリックします。

      ![](assets/input-form-create-4.png)

   1. フィールドを選択し、**[!UICONTROL OK]**&#x200B;をクリックします。

      ![](assets/input-form-create-5.png)

1. 必要に応じて、フィールドエディターを指定します。

   デフォルトのフィールドエディターは、各データタイプに関連付けられます。
   * 日付タイプフィールドの場合、フォームには入力カレンダーが表示されます。
   * 列挙タイプのフィールドの場合、フォームには選択リストが表示されます。

   次のフィールドエディタータイプを使用できます。

   | フィールドエディター | フォーム属性 |
   | --- | --- |
   | ラジオボタン | `type="radiobutton"` |
   | チェックボックス | `type="checkbox"` |
   | ツリーを編集 | `type="tree"` |

   詳しくは、[&#x200B; メモリリストコントロール &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#memory-list-controls){target="_blank"}を参照してください（Campaign v8 ドキュメント）。

1. オプションで、フィールドへのアクセスを定義します。

   | 要素 | 属性 | 説明 |
   | --- | --- | --- |
   | `<input>` | `read-only="true"` | フィールドへの読み取り専用アクセスを提供します |
   | `<container>` | `type="visibleGroup" visibleIf="`*edit-expr*`"` | 条件付きで表示されるフィールドグループ |
   | `<container>` | `type="enabledGroup" enabledIf="`*edit-expr*`"` | 条件付きでフィールドグループを有効にする |

   例：

   ```xml
   <container type="enabledGroup" enabledIf="@gender=1">
     […]
   </container>
   <container type="enabledGroup" enabledIf="@gender=2">
     […]
   </container>
   ```

1. 必要に応じて、コンテナを使用してフィールドをセクションにグループ化します。

   ```xml
   <container type="frame" label="Name">
      <input xpath="@firstName"/>
      <input xpath="@lastName"/>
   </container>
   <container type="frame" label="Contact details">
      <input xpath="@email"/>
      <input xpath="@phone"/>
   </container>
   ```

   ![](assets/input-form-create-3.png)

## 複数ページフォームの作成 {#create-multipage-form}

複数のページフォームを作成できます。 他のフォーム内にフォームをネストすることもできます。 [&#x200B; コンテナ、ノートブック、アイコンボックスフォーム &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#containers){target="_blank"}の詳細をご覧ください（Campaign v8 ドキュメント）。

## 工場出荷時の入力フォームの変更 {#modify-factory-form}

ファクトリフォームを変更するには、次の手順に従います。

1. 工場出荷時の入力フォームを変更します。

   1. メニューから、**[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**&#x200B;を選択します。
   1. 入力フォームを選択して修正します。

   ファクトリ データ スキーマを拡張することはできますが、ファクトリ入力フォームを拡張することはできません。 ファクトリ入力フォームを再作成することなく、直接変更することをお勧めします。 ソフトウェアのアップグレード時に、工場出荷時の入力フォームの変更がアップグレードと結合されます。 自動結合が失敗した場合は、競合を解決できます。 [詳細情報](../../production/using/upgrading.md#resolving-conflicts)。

   例えば、追加フィールドを含むファクトリスキーマを拡張する場合、このフィールドを関連するファクトリフォームに追加できます。

## フォームの検証 {#validate-forms}

フォームに検証コントロールを含めることができます。

### 必須フィールドの確認

次の必須情報を確認できます。

* 必須フィールドには`required="true"`属性を使用します。
* `<leave>` ノードを使用して、これらのフィールドを確認し、エラーメッセージを表示します。

この例では、電子メールアドレスが必要で、ユーザーがこの情報を提供していない場合はエラーメッセージが表示されます。

```xml
<input xpath="@email" required="true"/>
<leave>
  <check expr="@email!=''">
    <error>The email address is required.</error>
  </check>
</leave>
```

[式フィールド &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#expression-field){target="_blank"} （Campaign v8 ドキュメント）と[&#x200B; フォームコンテキスト &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#context-of-forms){target="_blank"} （Campaign v8 ドキュメント）について詳しく説明します。

### 値の検証

JavaScript SOAP呼び出しを使用して、コンソールからフォームデータを検証できます。 これらの呼び出しを使用して複雑な検証を行います。例えば、値を承認済み値のリストと照合します。 [詳細情報](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#soap-methods){target="_blank"}（Campaign v8 ドキュメント）。

1. JS ファイルに検証関数を作成します。

   例：

   ```js
   function nms_recipient_checkValue(value)
   {
     logInfo("checking value " + value)
     if (…)
     {
       logError("Value " + value + " is not valid")
     }
     return 1
   }
   ```

   この例では、関数の名前は`checkValue`です。 この関数は、`nms`名前空間の`recipient` データ型を確認するために使用されます。 チェックされている値がログに記録されます。 値が無効な場合は、エラーメッセージがログに記録されます。 値が有効な場合は、値1が返されます。

   返された値を使用して、フォームを変更できます。

1. フォームで、`<soapCall>`要素を`<leave>`要素に追加します。

   この例では、SOAP呼び出しを使用して`@valueToCheck`文字列を検証します。

   ```xml
   <form name="recipient" (…)>
   (…)
     <leave>
       <soapCall name="checkValue" service="nms:recipient">
         <param exprIn="@valueToCheck" type="string"/>
       </soapCall>
     </leave>
   </form>
   ```

   この例では、`checkValue` メソッドと`nms:recipient` サービスが使用されています。

   * サービスは名前空間とデータタイプです。
   * メソッドは関数名です。 名前では大文字と小文字が区別されます。

   呼び出しは同期して実行されます。

   すべての例外が表示されます。 `<leave>`要素を使用する場合、入力された情報が検証されるまで、ユーザーはフォームを保存できません。

次の例では、フォーム内からサービス呼び出しを行う方法を示します。

```xml
<enter>
  <soapCall name="client" service="c4:ybClient">
    <param exprIn="@id" type="string"/>
    <param type="boolean" xpathOut="/tmp/@count"/>
  </soapCall>
</enter>
```

この例では、入力はプライマリキーであるIDです。 ユーザーがこのIDのフォームに入力すると、このIDを入力パラメーターとしてSOAP呼び出しが行われます。 出力はこのフィールドに書き込まれるブール値です：`/tmp/@count`。 このブール値はフォーム内で使用できます。 [&#x200B; フォームコンテキスト &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms#context-of-forms){target="_blank"}の詳細（Campaign v8 ドキュメント）を参照してください。
