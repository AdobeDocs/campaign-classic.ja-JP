---
product: campaign
title: フォームの編集
description: フォームの編集
feature: Configuration
role: Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 24604dc9-f675-4e37-a848-f1911be84f3e
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 3%

---


# フォームの編集{#editing-forms}

## 概要

マーケターとオペレーターは、入力フォームを使用して、レコードを作成、変更およびプレビューします。 Formsは、情報を視覚的に表現します。

入力フォームを作成および変更できます。

* デフォルトで配信されるファクトリ入力フォームを変更できます。 ファクトリ入力フォームは、ファクトリデータスキーマに基づいています。
* 定義するデータスキーマに基づいて、カスタム入力フォームを作成できます。

Formsは `xtk:form` タイプのエンティティです。 `xtk:form` スキーマで入力フォーム構造を表示できます。 このスキーマを表示するには、メニューから **[!UICONTROL 管理]**/**[!UICONTROL 設定]**/**[!UICONTROL データスキーマ]** を選択します。 詳しくは、[&#x200B; フォーム構造 &#x200B;](form-structure.md) を参照してください。

入力フォームにアクセスするには、メニューから **[!UICONTROL 管理 &#x200B;]/[!UICONTROL &#x200B; 設定 &#x200B;]/[!UICONTROL &#x200B; 入力フォーム]** を選択します。

![](assets/d_ncs_integration_form_arbo.png)

フォームをデザインするには、XML エディターで XML コンテンツを編集します。

![](assets/d_ncs_integration_form_edit.png)

[詳細情報](form-structure.md#formatting)。

フォームをプレビューするには、「**[!UICONTROL プレビュー]**」タブをクリックします。

![](assets/d_ncs_integration_form_preview.png)

## フォームタイプ

様々なタイプの入力フォームを作成できます。 フォームタイプは、ユーザーによるフォームのナビゲーション方法を決定します。

* コンソール画面

  これはデフォルトのフォームタイプです。 フォームは単一のページで構成されます。

  ![](assets/console_screen_form.png)

* コンテンツ管理

  このフォームタイプをコンテンツ管理に使用します。 この [&#x200B; ユースケース &#x200B;](../../delivery/using/use-case-creating-content-management.md) を参照してください。

  ![](../../delivery/using/assets/d_ncs_content_form13.png)

* アシスタント

  このフォームは、特定のシーケンスで順序付けられた複数のフローティングスクリーンで構成されます。 ユーザーは、ある画面から次の画面に移動します。 [詳細情報](form-structure.md#wizards)。

* アイコンボックス

  このフォームは複数のページで構成されます。 フォームに移動するには、フォームの左側にあるアイコンを選択します。

  ![](assets/iconbox_form_preview.png)

* ノートブック

  このフォームは複数のページで構成されます。 フォームを移動するには、ユーザーがフォーム上部のタブを選択します。

  ![](assets/notebook_form_preview.png)

* 縦長ペイン

  このフォームには、ナビゲーションツリーが表示されます。

* 横長ペイン

  このフォームは、項目のリストを表示します。

## コンテナ

フォームでは、様々な目的でコンテナを使用できます。

* フォーム内のコンテンツの整理
* 入力フィールドへのアクセスの定義
* フォームを他のフォーム内にネスト

[詳細情報](form-structure.md#containers)。

### コンテンツを整理

コンテナを使用したフォーム内のコンテンツの整理：

* フィールドをセクションにグループ化できます。
* 複数ページのフォームにページを追加できます。

コンテナを挿入するには、`<container>` 要素を使用します。 [詳細情報](form-structure.md#containers)。

#### グループフィールド

コンテナを使用して、入力フィールドを整理されたセクションにグループ化します。

セクションをフォームに挿入するには、要素 `<container type="frame">` を使用します。 オプションで、セクションのタイトルを追加するには、`label` 属性を使用します。

構文：`<container type="frame" label="`*section_title*`"> […] </container>`

この例では、コンテナは、**作成者** および **[!UICONTROL 名前]** 入力フィールドで構成される **[!UICONTROL 作成]** セクションを定義します。

```xml
<form _cs="Coupons (nms)" entitySchema="xtk:form" img="xtk:form.png" label="Coupons"
      name="coupon" namespace="nms" type="default" xtkschema="xtk:form">
  <input xpath="@code"/>
  <input xpath="@type"/>
  <container label="Creation" type="frame">
    <input xpath="createdBy"/>
    <input xpath="createdBy/@name"/>
  </container>
</form>
```

![](assets/console_screen_form.png)

#### 複数ページフォームへのページの追加

複数ページフォームの場合、コンテナを使用してフォームページを作成します。

この例では、フォームの **一般** ページと **詳細** ページのコンテナを示します。

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

### フィールドへのアクセスの定義

コンテナを使用して、表示内容を定義し、フィールドへのアクセスを定義します。 フィールドのグループのオンとオフを切り替えることができます。

### フォームをネスト

コンテナを使用して、フォームを他のフォーム内にネストします。 [詳細情報](#add-pages-to-multipage-forms)。

## 画像への参照

画像を検索するには、メニューから **[!UICONTROL 管理]**/**[!UICONTROL 設定]**/**[!UICONTROL 画像]** を選択します。

画像をフォーム内の要素（アイコンなど）に関連付けるには、画像への参照を追加します。 `img` 属性を使用します（例：`<container>` 要素）。

構文：`img="`*`namespace`*`:`*`filename`*`.`*`extension`*`"`

この例では、`book.png` への参照と `detail.png` 名前空間からの `ncm` 画像を示します。

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

これらの画像は、ユーザーがクリックして複数ページのフォームを移動するためのアイコンに使用されます。

![](assets/nested_forms_preview.png)


## シンプルなフォームの作成 {#create-simple-form}

フォームを作成するには、次の手順に従います。

1. メニューから **[!UICONTROL 管理]**/**[!UICONTROL 設定]**/**[!UICONTROL 入力フォーム]** を選択します。
1. リストの右上にある「**[!UICONTROL 新規]** ボタンをクリックします。

   ![](assets/input-form-create-1.png)

1. フォームのプロパティを指定します。

   * フォーム名と名前空間を指定します。

     フォーム名と名前空間は、関連するデータスキーマと一致させることができます。  この例では、`cus:order` のデータスキーマ用のフォームを示します。

     ```xml
     <form entitySchema="xtk:form" img="xtk:form.png" label="Order" name="order" namespace="cus" type="iconbox" xtkschema="xtk:form">
       […]
     </form>
     ```

     または、`entity-schema` 属性でデータスキーマを明示的に指定できます。

     ```xml
     <form entity-schema="cus:stockLine" entitySchema="xtk:form" img="xtk:form.png" label="Stock order" name="stockOrder" namespace="cus" xtkschema="xtk:form">
       […]
     </form>
     ```

   * フォームに表示するラベルを指定します。
   * オプションで、フォームタイプを指定します。 フォームタイプを指定しない場合、コンソール画面タイプがデフォルトで使用されます。

     ![](assets/input-form-create-2.png)

     複数ページのフォームをデザインする場合、`<form>` 要素のフォームタイプを省略し、コンテナ内でタイプを指定できます。

1. 「**[!UICONTROL 保存]**」をクリックします。

1. フォーム要素を挿入します。

   例えば、入力フィールドを挿入するには、`<input>` 要素を使用します。 フィールド参照の `xpath` 属性を XPath 式として設定します。 [詳細情報](schema-structure.md#referencing-with-xpath)。

   この例では、`nms:recipient` スキーマに基づく入力フィールドを示します。

   ```xml
   <input xpath="@firstName"/>
   <input xpath="@lastName"/>
   ```

1. フォームが特定のスキーマタイプに基づいている場合は、このスキーマのフィールドを検索できます。

   1. **[!UICONTROL 挿入]**/**[!UICONTROL ドキュメントフィールド]** をクリックします。

      ![](assets/input-form-create-4.png)

   1. フィールドを選択して、「**[!UICONTROL OK]**」をクリックします。

      ![](assets/input-form-create-5.png)

1. オプションで、フィールドエディターを指定します。

   デフォルトのフィールドエディターは、各データタイプに関連付けられています。
   * 日付タイプのフィールドの場合、フォームには入力カレンダーが表示されます。
   * 列挙タイプのフィールドの場合、フォームに選択リストが表示されます。

   次のフィールドエディタータイプを使用できます。

   | フィールドエディター | フォーム属性 |
   | --- | --- |
   | ラジオボタン | `type="radiobutton"` |
   | チェックボックス | `type="checkbox"` |
   | ツリーを編集 | `type="tree"` |

   詳しくは、[&#x200B; メモリリストコントロール &#x200B;](form-structure.md#memory-list-controls) を参照してください。

1. オプションで、フィールドへのアクセスを定義します。

   | 要素 | 属性 | 説明 |
   | --- | --- | --- |
   | `<input>` | `read-only="true"` | フィールドへの読み取り専用アクセスを提供 |
   | `<container>` | `type="visibleGroup" visibleIf="`*edit-expr*`"` | フィールドのグループを条件付きで表示 |
   | `<container>` | `type="enabledGroup" enabledIf="`*edit-expr*`"` | フィールドのグループを条件付きで有効にします |

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

複数ページのフォームを作成できます。 フォームを他のフォーム内にネストすることもできます。

### `iconbox` フォームの作成

`iconbox` フォームタイプを使用して、フォームの左側に、フォーム内の様々なページにユーザーを移動するためのアイコンを表示します。

![](assets/iconbox_form_preview.png)

既存のフォームのタイプを `iconbox` に変更するには、次の手順に従います。

1. `type` 要素の `<form>` 属性を `iconbox` に変更します。

   ```xml
   <form […] type="iconbox">
   ```

1. 各フォームページにコンテナを設定します。

   1. `<container>` 要素を `<form>` 要素の子として追加します。
   1. アイコンのラベルと画像を定義するには、`label` 属性と `img` 属性を使用します。

      ```xml
      <form entitySchema="xtk:form" name="Service provider" namespace="nms" type="iconbox" xtkschema="xtk:form">
          <container img="xtk:properties.png" label="General">
              <input xpath="@label"/>
              <input xpath="@name"/>
              […]
          </container>
          <container img="nms:msgfolder.png" label="Details">
              <input xpath="@address"/>
              […]
          </container>
          <container img="nms:supplier.png" label="Services">
              […]
          </container>
      </form>
      ```

   または、既存の `type="frame"` 要素から `<container>` 属性を削除します。

### ノートブックフォームの作成

`notebook` のフォームタイプを使用して、ユーザーを別のページに移動させるタブをフォームの上部に表示します。

![](assets/notebook_form_preview.png)

既存のフォームのタイプを `notebook` に変更するには、次の手順に従います。

1. `type` 要素の `<form>` 属性を `notebook` に変更します。

   ```xml
   <form […] type="notebook">
   ```

1. 各フォームページにコンテナを追加します。

   1. `<container>` 要素を `<form>` 要素の子として追加します。
   1. アイコンのラベルと画像を定義するには、`label` 属性と `img` 属性を使用します。

   ```xml
     <form entitySchema="xtk:form" name="Service provider" namespace="nms" type="notebook" xtkschema="xtk:form">
         <container label="General">
             <input xpath="@label"/>
             <input xpath="@name"/>
             […]
         </container>
         <container label="Details">
             <input xpath="@address"/>
             […]
         </container>
         <container label="Services">
             […]
         </container>
     </form>
   ```

   または、既存の `type="frame"` 要素から `<container>` 属性を削除します。

### フォームをネスト

フォームは他のフォーム内にネストできます。 例えば、iconbox フォーム内にノートブックフォームをネストできます。

ネストのレベルによってナビゲーションが制御されます。 ユーザーは、サブフォームにドリルダウンできます。

フォームを別のフォーム内にネストするには、`<container>` 要素を挿入し、`type` 属性をフォームタイプに設定します。 最上位レベルのフォームの場合、外側のコンテナまたは `<form>` 要素でフォームタイプを設定できます。

### 例

この例では、複雑なフォームを示しています。

* 最上位のフォームは iconbox フォームです。 このフォームは、「一般 **および** 詳細 **というラベルの付いた 2 つのコンテナで構成さ** ます。

  その結果、外側のフォームには、**一般** ページと **詳細** ページが最上位に表示されます。 これらのページにアクセスするには、フォームの左側にあるアイコンをクリックします。

* サブフォームは、（一般 **コンテナ内にネストされたノートブックフォーム** す。 サブフォームは、「名前 **および** 連絡先 **というラベルが付いた 2 つのコンテナで構成さ** ます。

```xml
<form _cs="Profile (nms)" entitySchema="xtk:form" img="xtk:form.png" label="Profile" name="profile" namespace="nms" xtkschema="xtk:form">
  <container type="iconbox">
    <container img="ncm:general.png" label="General">
      <container type="notebook">
        <container label="Name">
          <input xpath="@firstName"/>
          <input xpath="@lastName"/>
        </container>
        <container label="Contact">
          <input xpath="@email"/>
        </container>
      </container>
    </container>
    <container img="ncm:detail.png" label="Details">
      <input xpath="@birthDate"/>
    </container>
  </container>
</form>
```

その結果、外側のフォームの **一般** ページには「**名前** タブと **連絡先** タブが表示されます。

![](assets/nested_forms_preview.png)

フォームを別のフォーム内にネストするには、`<container>` 要素を挿入し、`type` 属性をフォームタイプに設定します。 最上位レベルのフォームの場合、外側のコンテナまたは `<form>` 要素でフォームタイプを設定できます。

### 例

この例では、複雑なフォームを示しています。

* 最上位のフォームは iconbox フォームです。 このフォームは、「一般 **および** 詳細 **というラベルの付いた 2 つのコンテナで構成さ** ます。

  その結果、外側のフォームには、**一般** ページと **詳細** ページが最上位に表示されます。 これらのページにアクセスするには、フォームの左側にあるアイコンをクリックします。

* サブフォームは、（一般 **コンテナ内にネストされたノートブックフォーム** す。 サブフォームは、「名前 **および** 連絡先 **というラベルが付いた 2 つのコンテナで構成さ** ます。

```xml
<form _cs="Profile (nms)" entitySchema="xtk:form" img="xtk:form.png" label="Profile" name="profile" namespace="nms" xtkschema="xtk:form">
  <container type="iconbox">
    <container img="ncm:general.png" label="General">
      <container type="notebook">
        <container label="Name">
          <input xpath="@firstName"/>
          <input xpath="@lastName"/>
        </container>
        <container label="Contact">
          <input xpath="@email"/>
        </container>
      </container>
    </container>
    <container img="ncm:detail.png" label="Details">
      <input xpath="@birthDate"/>
    </container>
  </container>
</form>
```

その結果、外側のフォームの **一般** ページには「**名前** タブと **連絡先** タブが表示されます。

![](assets/nested_forms_preview.png)



## ファクトリ入力フォームの変更 {#modify-factory-form}

ファクトリフォームを変更するには、次の手順に従います。

1. ファクトリ入力フォームを次のように変更します。

   1. メニューから **[!UICONTROL 管理]**/**[!UICONTROL 設定]**/**[!UICONTROL 入力フォーム]** を選択します。
   1. 入力フォームを選択して変更します。

   ファクトリデータスキーマは拡張できますが、ファクトリ入力フォームは拡張できません。 ファクトリ入力フォームを再作成せずに、直接変更することをお勧めします。 ソフトウェアのアップグレード中に、工場出荷時の入力フォームに加えた変更は、アップグレードと結合されます。 自動結合が失敗した場合は、競合を解決できます。 [詳細情報](../../production/using/upgrading.md#resolving-conflicts)。

   例えば、フィールドを追加してファクトリスキーマを拡張する場合、このフィールドを関連するファクトリフォームに追加できます。

## フォームの検証 {#validate-forms}

フォームに検証コントロールを含めることができます。

### フィールドへの読み取り専用アクセスの許可

フィールドへの読み取り専用アクセスを許可するには、`readOnly="true"` 属性を使用します。 たとえば、レコードの主キーを読み取り専用アクセスで表示する場合があります。 [詳細情報](form-structure.md#non-editable-fields)。

この例では、`iRecipientId` スキーマのプライマリキー（`nms:recipient`）は読み取り専用アクセスで表示されます。

```xml
<value xpath="@iRecipientId" readOnly="true"/>
```

### 必須フィールドを確認

必須情報を確認できます。

* 必須フィールドには `required="true"` 属性を使用します。
* `<leave>` ノードを使用してこれらのフィールドを確認し、エラーメッセージを表示します。

この例では、メールアドレスは必須で、ユーザーがこの情報を指定していない場合、エラーメッセージが表示されます。

```xml
<input xpath="@email" required="true"/>
<leave>
  <check expr="@email!=''">
    <error>The email address is required.</error>
  </check>
</leave>
```

詳しくは、[&#x200B; 式フィールド &#x200B;](form-structure.md#expression-field) および [&#x200B; フォームコンテキスト &#x200B;](form-structure.md#context-of-forms) を参照してください。

### 値を検証

JavaScript SOAP呼び出しを使用して、コンソールからフォームデータを検証できます。 これらの呼び出しを使用して、複雑な検証を行います。例えば、許可された値のリストに対して値を確認する場合などに使用します。 [詳細情報](form-structure.md#soap-methods)。

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

   この例では、関数の名前は `checkValue` です。 この関数は、`recipient` 名前空間の `nms` データタイプを確認するために使用されます。 チェックされる値はログに記録されます。 値が有効でない場合は、エラーメッセージがログに記録されます。 値が有効な場合は、値 1 が返されます。

   戻り値を使用してフォームを変更できます。

1. フォームで、`<soapCall>` 要素を `<leave>` 要素に追加します。

   この例では、SOAP呼び出しを使用して `@valueToCheck` の文字列を検証します。

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

   この例では、`checkValue` メソッドと `nms:recipient` サービスを使用します。

   * サービスは名前空間であり、データタイプです。
   * メソッドは関数名です。 この名前では大文字と小文字が区別されます。

   呼び出しは同期的に実行されます。

   すべての例外が表示されます。 `<leave>` 要素を使用する場合、入力した情報が検証されるまで、ユーザーはフォームを保存できません。

次の例では、フォーム内からサービス呼び出しを行う方法を示しています。

```xml
<enter>
  <soapCall name="client" service="c4:ybClient">
    <param exprIn="@id" type="string"/>
    <param type="boolean" xpathOut="/tmp/@count"/>
  </soapCall>
</enter>
```

この例では、入力は ID （プライマリキー）です。 ユーザーがこの ID のフォームに入力すると、この ID を入力パラメーターとしてSOAPが呼び出されます。 出力は、このフィールド `/tmp/@count` に書き込まれるブール値です。 このブール値をフォーム内で使用できます。 詳しくは、[&#x200B; フォームコンテキスト &#x200B;](form-structure.md#context-of-forms) を参照してください。
