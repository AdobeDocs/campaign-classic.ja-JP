---
product: campaign
title: フォームの編集
description: フォームの編集
feature: Configuration
role: Data Engineer, Developer
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 24604dc9-f675-4e37-a848-f1911be84f3e
source-git-commit: 668cee663890fafe27f86f2afd3752f7e2ab347a
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 3%

---


# フォームの編集{#editing-forms}

## 概要

マーケターやオペレーターは、入力フォームを使用して、レコードの作成、変更、プレビューをおこないます。 Formsは、情報を視覚的に表現します。

入力フォームを作成および変更できます。

* デフォルトで配信されるファクトリ入力フォームを変更できます。 ファクトリの入力フォームは、ファクトリデータスキーマに基づいています。
* 定義したデータスキーマに基づいて、カスタムの入力フォームを作成できます。

Formsは `xtk:form` タイプ。 入力フォームの構造は、 `xtk:form` スキーマ。 このスキーマを表示するには、 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]** を選択します。 詳細を表示： [フォーム構造](form-structure.md).

入力フォームにアクセスするには、「 **[!UICONTROL 管理] > [!UICONTROL 設定] > [!UICONTROL 入力フォーム]** メニューから、次の操作を実行します。

![](assets/d_ncs_integration_form_arbo.png)

フォームをデザインするには、XML エディターで XML コンテンツを編集します。

![](assets/d_ncs_integration_form_edit.png)

[詳細情報](form-structure.md#formatting)。

フォームをプレビューするには、 **[!UICONTROL プレビュー]** タブ：

![](assets/d_ncs_integration_form_preview.png)

## フォームタイプ

様々なタイプの入力フォームを作成できます。 フォームの種類によって、ユーザーによるフォームのナビゲーション方法が決まります。

* コンソール画面

  これはデフォルトのフォームタイプです。 フォームは単一のページで構成されます。

  ![](assets/console_screen_form.png)

* コンテンツ管理

  このフォームタイプをコンテンツ管理に使用します。 詳しくは、 [使用例](../../delivery/using/use-case-creating-content-management.md).

  ![](../../delivery/using/assets/d_ncs_content_form13.png)

* ウィザード

  このフォームは、特定のシーケンスで並べられた複数のフローティングスクリーンで構成されます。 ユーザーは画面間を移動します。 [詳細情報](form-structure.md#wizards)。

* アイコンボックス

  このフォームは複数のページで構成されます。 フォームに移動するには、フォームの左側でアイコンを選択します。

  ![](assets/iconbox_form_preview.png)

* ノートブック

  このフォームは複数のページで構成されます。 フォームに移動するには、フォーム上部のタブを選択します。

  ![](assets/notebook_form_preview.png)

* 縦長ペイン

  このフォームは、ナビゲーションツリーを表示します。

* 横長ペイン

  このフォームは、項目のリストを表示します。

## コンテナ

フォームでは、次のような様々な目的でコンテナを使用できます。

* フォーム内のコンテンツを整理する
* 入力フィールドへのアクセスを定義する
* 他のフォーム内でのフォームのネスト

[詳細情報](form-structure.md#containers)。

### コンテンツを整理

コンテナを使用してフォーム内のコンテンツを整理する：

* フィールドを複数のセクションにグループ化できます。
* 複数ページのフォームにページを追加できます。

コンテナを挿入するには、 `<container>` 要素を選択します。 [詳細情報](form-structure.md#containers)。

#### グループフィールド

コンテナを使用して、入力フィールドを整理されたセクションにグループ化します。

フォームにセクションを挿入するには、次の要素を使用します。 `<container type="frame">`. （オプション）セクションタイトルを追加するには、 `label` 属性。

構文： `<container type="frame" label="`*section_title*`"> […] </container>`

この例では、コンテナによって **作成** セクション ( **[!UICONTROL 作成者]** および **[!UICONTROL 名前]** 入力フィールド：

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

#### 複数ページのフォームにページを追加

複数ページフォームの場合は、コンテナを使用してフォームページを作成します。

この例では、 **一般** および **詳細** フォームのページ：

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

### フィールドへのアクセスを定義

コンテナを使用して、表示内容を定義し、フィールドへのアクセスを定義します。 フィールドのグループのオン/オフを切り替えることができます。

### フォームのネスト

コンテナを使用して、他のフォーム内にフォームをネストします。 [詳細情報](#add-pages-to-multipage-forms)。

## 画像への参照

画像を検索するには、「 」を選択します。 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 画像]** を選択します。

画像をフォーム内の要素（アイコンなど）に関連付けるには、画像への参照を追加します。 以下を使用します。 `img` 属性 ( 例： `<container>` 要素を選択します。

構文： `img="`*`namespace`*`:`*`filename`*`.`*`extension`*`"`

この例では、 `book.png` および `detail.png` 画像 `ncm` 名前空間：

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

1. メニューから、「 」を選択します。 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**.
1. 次をクリック： **[!UICONTROL 新規]** 」ボタンをクリックします。

   ![](assets/input-form-create-1.png)

1. フォームのプロパティを指定します。

   * フォーム名と名前空間を指定します。

     フォーム名と名前空間は、関連するデータスキーマと一致させることができます。  この例では、 `cus:order` データスキーマ：

     ```xml
     <form entitySchema="xtk:form" img="xtk:form.png" label="Order" name="order" namespace="cus" type="iconbox" xtkschema="xtk:form">
       […]
     </form>
     ```

     または、 `entity-schema` 属性。

     ```xml
     <form entity-schema="cus:stockLine" entitySchema="xtk:form" img="xtk:form.png" label="Stock order" name="stockOrder" namespace="cus" xtkschema="xtk:form">
       […]
     </form>
     ```

   * フォームに表示するラベルを指定します。
   * 必要に応じて、フォームタイプを指定します。 フォームタイプを指定しない場合、コンソール画面タイプがデフォルトで使用されます。

     ![](assets/input-form-create-2.png)

     複数ページのフォームをデザインする場合は、 `<form>` 要素を選択して、コンテナのタイプを指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

1. フォーム要素を挿入します。

   例えば、入力フィールドを挿入するには、 `<input>` 要素を選択します。 を設定します。 `xpath` 属性を XPath 式としてフィールド参照に追加します。 [詳細情報](schema-structure.md#referencing-with-xpath)。

   この例では、 `nms:recipient` スキーマ。

   ```xml
   <input xpath="@firstName"/>
   <input xpath="@lastName"/>
   ```

1. フォームが特定のスキーマタイプに基づいている場合は、このスキーマのフィールドを検索できます。

   1. クリック **[!UICONTROL 挿入]** > **[!UICONTROL ドキュメントフィールド]**.

      ![](assets/input-form-create-4.png)

   1. フィールドを選択し、 **[!UICONTROL OK]**.

      ![](assets/input-form-create-5.png)

1. 必要に応じて、フィールドエディターを指定します。

   デフォルトのフィールドエディターは、各データタイプに関連付けられています。
   * 日付タイプのフィールドの場合、フォームには入力カレンダーが表示されます。
   * 列挙タイプのフィールドの場合、フォームに選択リストが表示されます。

   次のタイプのフィールドエディターを使用できます。

   | フィールドエディター | フォーム属性 |
   | --- | --- |
   | ラジオボタン | `type="radiobutton"` |
   | チェックボックス | `type="checkbox"` |
   | ツリーを編集 | `type="tree"` |

   詳細を表示： [メモリリスト制御](form-structure.md#memory-list-controls).

1. オプションで、次のフィールドへのアクセスを定義します。

   | 要素 | 属性 | 説明 |
   | --- | --- | --- |
   | `<input>` | `read-only="true"` | フィールドへの読み取り専用アクセスを提供します |
   | `<container>` | `type="visibleGroup" visibleIf="`*edit-expr*`"` | 条件付きでフィールドのグループを表示します |
   | `<container>` | `type="enabledGroup" enabledIf="`*edit-expr*`"` | 条件に応じてフィールドのグループを有効にします |

   例：

   ```xml
   <container type="enabledGroup" enabledIf="@gender=1">
     […]
   </container>
   <container type="enabledGroup" enabledIf="@gender=2">
     […]
   </container>
   ```

1. オプションで、コンテナを使用してフィールドをセクションにグループ化します。

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

複数ページのフォームを作成できます。 また、他のフォーム内にフォームをネストすることもできます。

### の作成 `iconbox` フォーム

以下を使用します。 `iconbox` フォームの左側にアイコンを表示するフォームタイプ。このアイコンにより、ユーザーはフォーム内の別のページに移動できます。

![](assets/iconbox_form_preview.png)

既存のフォームの種類を次に変更するには `iconbox`を使用する場合は、次の手順に従います。

1. 次を変更： `type` の属性 `<form>` 要素から `iconbox`:

   ```xml
   <form […] type="iconbox">
   ```

1. 各フォームページにコンテナを設定します。

   1. を追加します。 `<container>` の子としての要素 `<form>` 要素を選択します。
   1. アイコンのラベルと画像を定義するには、 `label` および `img` 属性。

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

   または、 `type="frame"` 既存の属性 `<container>` 要素。

### ノートブックフォームの作成

以下を使用します。 `notebook` フォームの上部にタブを表示するフォームタイプ（ユーザーを別のページに移動させます）。

![](assets/notebook_form_preview.png)

既存のフォームの種類を次に変更するには `notebook`を使用する場合は、次の手順に従います。

1. 次を変更： `type` の属性 `<form>` 要素から `notebook`:

   ```xml
   <form […] type="notebook">
   ```

1. 各フォームページにコンテナを追加します。

   1. を追加します。 `<container>` の子としての要素 `<form>` 要素を選択します。
   1. アイコンのラベルと画像を定義するには、 `label` および `img` 属性。

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

   または、 `type="frame"` 既存の属性 `<container>` 要素。

### フォームのネスト

他のフォーム内にフォームをネストすることができます。 例えば、iconbox フォーム内でノートブックフォームをネストできます。

ネスト制御のレベル。 ユーザーはサブフォームにドリルダウンできます。

別のフォーム内にフォームをネストするには、 `<container>` 要素を選択し、 `type` 属性をフォームタイプに設定します。 トップレベルのフォームの場合は、外側のコンテナまたは `<form>` 要素を選択します。

### 例

次の例は、複雑なフォームを示しています。

* トップレベルフォームは、iconbox フォームです。 このフォームは、次のラベルが付いた 2 つのコンテナで構成されます。 **一般** および **詳細**.

  その結果、外側のフォームには **一般** および **詳細** ページを表示します。 これらのページにアクセスするには、ユーザーがフォームの左側にあるアイコンをクリックします。

* サブフォームは、 **一般** コンテナ。 サブフォームは、ラベル付けされた 2 つのコンテナで構成されます **名前** および **連絡先**.

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

その結果、 **一般** 外側のフォームのページは、 **名前** および **連絡先** タブ。

![](assets/nested_forms_preview.png)

別のフォーム内にフォームをネストするには、 `<container>` 要素を選択し、 `type` 属性をフォームタイプに設定します。 トップレベルのフォームの場合は、外側のコンテナまたは `<form>` 要素を選択します。

### 例

次の例は、複雑なフォームを示しています。

* トップレベルフォームは、iconbox フォームです。 このフォームは、次のラベルが付いた 2 つのコンテナで構成されます。 **一般** および **詳細**.

  その結果、外側のフォームには **一般** および **詳細** ページを表示します。 これらのページにアクセスするには、ユーザーがフォームの左側にあるアイコンをクリックします。

* サブフォームは、 **一般** コンテナ。 サブフォームは、ラベル付けされた 2 つのコンテナで構成されます **名前** および **連絡先**.

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

その結果、 **一般** 外側のフォームのページは、 **名前** および **連絡先** タブ。

![](assets/nested_forms_preview.png)



## ファクトリ入力フォームの変更 {#modify-factory-form}

ファクトリフォームを変更するには、次の手順に従います。

1. ファクトリ入力フォームを変更します。

   1. メニューから、「 」を選択します。 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**.
   1. 入力フォームを選択し、変更します。

   ファクトリデータスキーマは拡張できますが、ファクトリ入力フォームは拡張できません。 ファクトリの入力フォームは、再作成せずに直接変更することをお勧めします。 ソフトウェアのアップグレード時に、ファクトリの入力フォームでの変更内容とアップグレードが結合されます。 自動マージが失敗した場合は、競合を解決できます。 [詳細情報](../../production/using/upgrading.md#resolving-conflicts)。

   例えば、追加のフィールドを含むファクトリスキーマを拡張する場合、このフィールドを関連するファクトリフォームに追加できます。

## フォームの検証 {#validate-forms}

フォームに検証コントロールを含めることができます。

### フィールドへの読み取り専用アクセス権の付与

フィールドに読み取り専用アクセス権を付与するには、 `readOnly="true"` 属性。 例えば、読み取り専用アクセス権を持つレコードのプライマリキーを表示する場合があります。 [詳細情報](form-structure.md#non-editable-fields)。

この例では、プライマリキー (`iRecipientId`) `nms:recipient` スキーマは読み取り専用アクセスで表示されます。

```xml
<value xpath="@iRecipientId" readOnly="true"/>
```

### 必須フィールドを確認する

次の必須情報を確認できます。

* 以下を使用します。 `required="true"` 属性を設定します。
* 以下を使用します。 `<leave>` ノードを使用して、これらのフィールドを確認し、エラーメッセージを表示します。

この例では、電子メールアドレスが必要です。ユーザーがこの情報を指定しなかった場合は、エラーメッセージが表示されます。

```xml
<input xpath="@email" required="true"/>
<leave>
  <check expr="@email!=''">
    <error>The email address is required.</error>
  </check>
</leave>
```

詳細を表示： [式フィールド](form-structure.md#expression-field) および [フォームコンテキスト](form-structure.md#context-of-forms).

### 値の検証

JavaScript SOAP 呼び出しを使用して、コンソールからフォームデータを検証できます。 複雑な検証にこれらの呼び出しを使用して、例えば、許可された値のリストに対して値をチェックします。 [詳細情報](form-structure.md#soap-methods)。

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

   この例では、関数の名前はです。 `checkValue`. この関数は、 `recipient` データタイプ `nms` 名前空間。 確認中の値がログに記録されます。 値が無効な場合は、エラーメッセージが記録されます。 値が有効な場合は、値 1 が返されます。

   返された値を使用してフォームを変更できます。

1. フォームで、 `<soapCall>` 要素を `<leave>` 要素を選択します。

   この例では、SOAP 呼び出しを使用して `@valueToCheck` 文字列：

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

   この例では、 `checkValue` メソッドおよび `nms:recipient` サービスは次の場合に使用されます。

   * サービスは名前空間とデータ型です。
   * メソッドは関数名です。 名前では大文字と小文字が区別されます。

   呼び出しは同期的に実行されます。

   すべての例外が表示されます。 を使用する場合、 `<leave>` 要素を指定した場合、入力した情報が検証されるまでフォームを保存できません。

次の例では、フォーム内からサービス呼び出しを実行する方法を示します。

```xml
<enter>
  <soapCall name="client" service="c4:ybClient">
    <param exprIn="@id" type="string"/>
    <param type="boolean" xpathOut="/tmp/@count"/>
  </soapCall>
</enter>
```

この例では、入力は ID で、プライマリキーです。 ユーザーがこの ID のフォームに入力すると、この ID を入力パラメーターとして使用した SOAP 呼び出しがおこなわれます。 出力は、このフィールドに書き込まれるブール値です。 `/tmp/@count`. このブール値は、フォーム内で使用できます。 詳細を表示： [フォームコンテキスト](form-structure.md#context-of-forms).
