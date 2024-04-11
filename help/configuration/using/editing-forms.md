---
product: campaign
title: フォームの編集
description: フォームの編集
feature: Configuration
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 24604dc9-f675-4e37-a848-f1911be84f3e
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
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

Formsはのエンティティです `xtk:form` タイプ。 入力フォーム構造は、 `xtk:form` スキーマ。 このスキーマを表示するには、以下を選択します： **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]** メニューから。 詳細を読む： [フォーム構造](form-structure.md).

入力フォームにアクセスするには、を選択します **[!UICONTROL 管理] > [!UICONTROL 設定] > [!UICONTROL 入力フォーム]** メニューから：

![](assets/d_ncs_integration_form_arbo.png)

フォームをデザインするには、XML エディターで XML コンテンツを編集します。

![](assets/d_ncs_integration_form_edit.png)

[詳細情報](form-structure.md#formatting)。

フォームをプレビューするには、をクリックします **[!UICONTROL プレビュー]** タブ：

![](assets/d_ncs_integration_form_preview.png)

## フォームタイプ

様々なタイプの入力フォームを作成できます。 フォームタイプは、ユーザーによるフォームのナビゲーション方法を決定します。

* コンソール画面

  これはデフォルトのフォームタイプです。 フォームは単一のページで構成されます。

  ![](assets/console_screen_form.png)

* コンテンツ管理

  このフォームタイプをコンテンツ管理に使用します。 これを表示 [ユースケース](../../delivery/using/use-case-creating-content-management.md).

  ![](../../delivery/using/assets/d_ncs_content_form13.png)

* ウィザード

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

コンテナを挿入するには、 `<container>` 要素。 [詳細情報](form-structure.md#containers)。

#### グループフィールド

コンテナを使用して、入力フィールドを整理されたセクションにグループ化します。

セクションをフォームに挿入するには、次の要素を使用します。 `<container type="frame">`. 必要に応じて、セクションのタイトルを追加するには、 `label` 属性。

構文： `<container type="frame" label="`*section_title*`"> […] </container>`

この例では、コンテナは以下を定義します。 **作成** セクション。次で構成されます **[!UICONTROL 作成者]** および **[!UICONTROL 名前]** 入力フィールド：

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

この例は、のコンテナを示しています **一般** および **詳細** フォームのページ：

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

画像を検索するには、を選択します **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 画像]** メニューから。

画像をフォーム内の要素（アイコンなど）に関連付けるには、画像への参照を追加します。 の使用 `img` 属性（例：） `<container>` 要素。

構文： `img="`*`namespace`*`:`*`filename`*`.`*`extension`*`"`

この例では、への参照を示しています `book.png` および `detail.png` からの画像 `ncm` 名前空間：

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

1. メニューから次を選択します **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**.
1. 「」をクリックします **[!UICONTROL 新規]** ボタンをクリックします。

   ![](assets/input-form-create-1.png)

1. フォームのプロパティを指定します。

   * フォーム名と名前空間を指定します。

     フォーム名と名前空間は、関連するデータスキーマと一致させることができます。  この例では、のフォームを示します `cus:order` データスキーマ：

     ```xml
     <form entitySchema="xtk:form" img="xtk:form.png" label="Order" name="order" namespace="cus" type="iconbox" xtkschema="xtk:form">
       […]
     </form>
     ```

     または、データスキーマを明示的に指定することもできます `entity-schema` 属性。

     ```xml
     <form entity-schema="cus:stockLine" entitySchema="xtk:form" img="xtk:form.png" label="Stock order" name="stockOrder" namespace="cus" xtkschema="xtk:form">
       […]
     </form>
     ```

   * フォームに表示するラベルを指定します。
   * オプションで、フォームタイプを指定します。 フォームタイプを指定しない場合、コンソール画面タイプがデフォルトで使用されます。

     ![](assets/input-form-create-2.png)

     複数ページフォームをデザインする場合、のフォームタイプを省略できます。 `<form>` 要素を選択し、コンテナ内のタイプを指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

1. フォーム要素を挿入します。

   例えば、入力フィールドを挿入するには、 `<input>` 要素。 を `xpath` フィールド参照の属性を XPath 式として指定します。 [詳細情報](schema-structure.md#referencing-with-xpath)。

   この例では、に基づく入力フィールドを示しています `nms:recipient` スキーマ。

   ```xml
   <input xpath="@firstName"/>
   <input xpath="@lastName"/>
   ```

1. フォームが特定のスキーマタイプに基づいている場合は、このスキーマのフィールドを検索できます。

   1. クリック **[!UICONTROL 挿入]** > **[!UICONTROL ドキュメントフィールド]**.

      ![](assets/input-form-create-4.png)

   1. フィールドを選択し、 **[!UICONTROL OK]**.

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

   詳細を読む： [メモリリスト制御](form-structure.md#memory-list-controls).

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

### を作成 `iconbox` フォーム

の使用 `iconbox` フォームタイプ：フォームの左側にアイコンを表示します。このアイコンはユーザーをフォーム内の別のページに移動します。

![](assets/iconbox_form_preview.png)

既存のフォームのタイプをに変更するには `iconbox`は、次の手順に従います。

1. 変更： `type` 属性 `<form>` 要素の移動先 `iconbox`:

   ```xml
   <form […] type="iconbox">
   ```

1. 各フォームページにコンテナを設定します。

   1. を追加 `<container>` の子としての要素 `<form>` 要素。
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

   または、を削除します `type="frame"` 既存のの属性 `<container>` 要素。

### ノートブックフォームの作成

の使用 `notebook` フォームタイプ：フォームの上部にタブを表示します。これにより、ユーザーは様々なページに移動します。

![](assets/notebook_form_preview.png)

既存のフォームのタイプをに変更するには `notebook`は、次の手順に従います。

1. 変更： `type` 属性 `<form>` 要素の移動先 `notebook`:

   ```xml
   <form […] type="notebook">
   ```

1. 各フォームページにコンテナを追加します。

   1. を追加 `<container>` の子としての要素 `<form>` 要素。
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

   または、を削除します `type="frame"` 既存のの属性 `<container>` 要素。

### フォームをネスト

フォームは他のフォーム内にネストできます。 例えば、iconbox フォーム内にノートブックフォームをネストできます。

ネストのレベルによってナビゲーションが制御されます。 ユーザーは、サブフォームにドリルダウンできます。

フォームを別のフォーム内にネストするには、以下を挿入します `<container>` を要素にして、 `type` フォームタイプに対する属性。 最上位レベルのフォームの場合、外部コンテナまたは内のコンテナにフォームタイプを設定できます。 `<form>` 要素。

### 例

この例では、複雑なフォームを示しています。

* 最上位のフォームは iconbox フォームです。 このフォームは、「」というラベルの付いた 2 つのコンテナで構成されます **一般** および **詳細**.

  その結果、外側のフォームには次の内容が表示されます。 **一般** および **詳細** トップレベルのページ。 これらのページにアクセスするには、フォームの左側にあるアイコンをクリックします。

* サブフォームは、内にネストされたノートブックフォームです **一般** コンテナ。 サブフォームは、というラベルの 2 つのコンテナで構成されます **名前** および **連絡先**.

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

その結果、 **一般** 外側のフォームのページには、 **名前** および **連絡先** タブ。

![](assets/nested_forms_preview.png)

フォームを別のフォーム内にネストするには、以下を挿入します `<container>` を要素にして、 `type` フォームタイプに対する属性。 最上位レベルのフォームの場合、外部コンテナまたは内のコンテナにフォームタイプを設定できます。 `<form>` 要素。

### 例

この例では、複雑なフォームを示しています。

* 最上位のフォームは iconbox フォームです。 このフォームは、「」というラベルの付いた 2 つのコンテナで構成されます **一般** および **詳細**.

  その結果、外側のフォームには次の内容が表示されます。 **一般** および **詳細** トップレベルのページ。 これらのページにアクセスするには、フォームの左側にあるアイコンをクリックします。

* サブフォームは、内にネストされたノートブックフォームです **一般** コンテナ。 サブフォームは、というラベルの 2 つのコンテナで構成されます **名前** および **連絡先**.

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

その結果、 **一般** 外側のフォームのページには、 **名前** および **連絡先** タブ。

![](assets/nested_forms_preview.png)



## ファクトリ入力フォームの変更 {#modify-factory-form}

ファクトリフォームを変更するには、次の手順に従います。

1. ファクトリ入力フォームを次のように変更します。

   1. メニューから次を選択します **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 入力フォーム]**.
   1. 入力フォームを選択して変更します。

   ファクトリデータスキーマは拡張できますが、ファクトリ入力フォームは拡張できません。 ファクトリ入力フォームを再作成せずに、直接変更することをお勧めします。 ソフトウェアのアップグレード中に、工場出荷時の入力フォームに加えた変更は、アップグレードと結合されます。 自動結合が失敗した場合は、競合を解決できます。 [詳細情報](../../production/using/upgrading.md#resolving-conflicts)。

   例えば、フィールドを追加してファクトリスキーマを拡張する場合、このフィールドを関連するファクトリフォームに追加できます。

## フォームの検証 {#validate-forms}

フォームに検証コントロールを含めることができます。

### フィールドへの読み取り専用アクセスの許可

フィールドへの読み取り専用アクセスを許可するには、 `readOnly="true"` 属性。 たとえば、レコードの主キーを読み取り専用アクセスで表示する場合があります。 [詳細情報](form-structure.md#non-editable-fields)。

この例では、プライマリキー（`iRecipientId`） `nms:recipient` スキーマは読み取り専用アクセスで表示されます。

```xml
<value xpath="@iRecipientId" readOnly="true"/>
```

### 必須フィールドを確認

必須情報を確認できます。

* の使用 `required="true"` 必須フィールドの属性です。
* の使用 `<leave>` ノードを使用して、これらのフィールドを確認し、エラーメッセージを表示します。

この例では、メールアドレスは必須で、ユーザーがこの情報を指定していない場合、エラーメッセージが表示されます。

```xml
<input xpath="@email" required="true"/>
<leave>
  <check expr="@email!=''">
    <error>The email address is required.</error>
  </check>
</leave>
```

詳細を読む： [式のフィールド](form-structure.md#expression-field) および [フォームコンテキスト](form-structure.md#context-of-forms).

### 値を検証

JavaScript SOAP 呼び出しを使用して、コンソールからフォームデータを検証できます。 これらの呼び出しを使用して、複雑な検証を行います。例えば、許可された値のリストに対して値を確認する場合などに使用します。 [詳細情報](form-structure.md#soap-methods)。

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

   この例では、関数の名前はです `checkValue`. この関数は、 `recipient` 内のデータタイプ `nms` 名前空間。 チェックされる値はログに記録されます。 値が有効でない場合は、エラーメッセージがログに記録されます。 値が有効な場合は、値 1 が返されます。

   戻り値を使用してフォームを変更できます。

1. フォームで、を追加します `<soapCall>` 要素を `<leave>` 要素。

   この例では、SOAP 呼び出しを使用して、 `@valueToCheck` 文字列：

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

   この例では、 `checkValue` メソッドおよび `nms:recipient` 使用されるサービス：

   * サービスは名前空間であり、データタイプです。
   * メソッドは関数名です。 この名前では大文字と小文字が区別されます。

   呼び出しは同期的に実行されます。

   すべての例外が表示されます。 使用する場合 `<leave>` 入力された情報が検証されるまで、要素でフォームを保存することはできません。

次の例では、フォーム内からサービス呼び出しを行う方法を示しています。

```xml
<enter>
  <soapCall name="client" service="c4:ybClient">
    <param exprIn="@id" type="string"/>
    <param type="boolean" xpathOut="/tmp/@count"/>
  </soapCall>
</enter>
```

この例では、入力は ID （プライマリキー）です。 ユーザーがこの ID のフォームに入力すると、この ID を入力パラメーターとして SOAP 呼び出しが行われます。 出力は、このフィールドに書き込まれるブール値です。 `/tmp/@count`. このブール値をフォーム内で使用できます。 詳細を読む： [フォームコンテキスト](form-structure.md#context-of-forms).
