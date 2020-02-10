---
title: 入力フォーム
seo-title: 入力フォーム
description: 入力フォーム
seo-description: null
page-status-flag: never-activated
uuid: f7537707-3ea9-4afb-a4c1-4a985f62dbdf
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: abf097eb-ade5-479e-9e20-8bd6bc9d96aa
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# 入力フォーム{#input-forms}

Adobe Campaign の入力フォーム使用に関する一般的な原理を一部紹介します。

フォームについては、[この節](../../configuration/using/identifying-a-form.md)で詳しく説明しています。

## フォームの構造 {#form-structure}

The XML document of an input form must contain the **`<form>`** root element with the **name** and **namespace** attributes to populate the form name and its namespace, respectively.

```
<form name="form_name" namespace="name_space">
...
</form>
```

デフォルトでは、フォームは同じ名前と名前空間を持つデータスキーマに関連付けられます。To associate a form with a different name, enter the schema key in the **entity-schema** attribute of the **`<form>`** element.

入力フォームの構造を説明するために、サンプルのスキーマ「cus:book」をベースとするインターフェイスについて説明します。

![](assets/d_ncs_content_form1.png)

対応する入力フォームは次のようになります。

```
<form name="book" namespace="cus" type="contentForm">
  <input xpath="@name"/>
  <input xpath="@date"/>
  <input xpath="@language"/>
</form>
```

The description of the edit elements begins with the **`<form>`** root element.

An edit control is entered in an **`<input>`** element with the **xpath** attribute containing the path of the field in its schema.

**XPath 構文に関する注意：**

Adobe Campaign では、XPath 言語を使用して、データスキーマに属する要素または属性を参照します。

XPath は、XML ドキュメントのツリー内にノードを配置するための構文です。

要素は名前で指定し、属性は名前の前に「@」文字を付けて指定します。

例：

* **@date**：「date」という名前の属性を選択
* **chapter/@title**:要素の下に「title」属性を選択しま `<chapter>` す
* **../@date**：現在の要素の親要素から date を選択

編集コントロールは、対応するデータタイプに自動的に適応し、スキーマで定義されているラベルを使用します。

デフォルトでは、各フィールドが 1 行に表示され、データのタイプに応じて、すべての空きスペースを占有します。

>[!CAUTION]
>
>The input form must reference a **type=&quot;contentForm&quot;** attribute on the **`<form>`** element to automatically add the frame required for content to be input.

## 書式設定 {#formatting}

コントロールを互いに相対的に配置する作業は、HTML テーブルで使用される配置に似ています。1 つのコントロールを複数の列に分割したり、複数の要素を組み合わせたり、空きスペースの占有を指定したりできます。ただし、書式設定で許可されているのは割合の記述のみです。オブジェクトの固定寸法は指定できません。

詳しくは、[この節](../../configuration/using/form-structure.md#formatting)を参照してください。

## リストタイプのコントロール {#list-type-controls}

コレクション要素を編集するには、リストタイプのコントロールを使用する必要があります。

### 列リスト {#column-list}

このコントロールは、「追加」ボタンと「削除」ボタンを含むツールバー付きの編集可能な列リストを表示しています。

![](assets/d_ncs_content_form4.png)

```
<input xpath="chapter" type="list">
  <input xpath="@name"/>
  <input xpath="@number"/>
</input>
```

リストコントロールは、**type=&quot;list&quot;** 属性を使用して設定する必要があります。リストのパスは、コレクション要素を参照する必要があります。

The columns are declared by the child **`<input>`** elements of the list.

>[!NOTE]
>
>上と下の並べ替え矢印は、データスキーマ内のコレクション要素に **ordered=&quot;true&quot;** 属性を設定すると、自動的に追加されます。

デフォルトでは、ツールバーのボタンは垂直方向に整列されます。水平方向に整列させることもできます。

![](assets/d_ncs_content_form5.png)

```
<input nolabel="true" toolbarCaption="List of chapters" type="list" xpath="chapter">
  <input xpath="@name"/>
  <input xpath="@number"/>
</input>
```

**toolbarCaption** 属性は、ツールバーを水平方向に整列させ、リストの上のタイトルを設定します。

>[!NOTE]
>
>コントロールの左側にコレクション要素のラベルを表示しないようにするには、**nolabel=&quot;true&quot;** 属性を追加します。

#### リストの詳細表示 {#zoom-in-a-list}

リストデータの挿入と編集は、別々の編集フォームで実行できます。

リスト内の編集フォームは、次のような場合に使用します。

* 情報入力を簡単にする
* 複数行コントロールが存在する
* リスト内の列にメインフィールドのみ含め、フォームでコレクション要素のすべてのフィールドを表示する

![](assets/d_ncs_content_form7.png)

```
<input nolabel="true" toolbarCaption="List of chapters" type="list" xpath="chapter" zoom="true" zoomOnAdd="true">
  <input xpath="@name"/>
  <input xpath="@number"/>

  <form colcount="2" label="Editing a chapter">
    <input xpath="@name"/>
    <input xpath="@number"/>
    <input colspan="2" xpath="page"/>
  </form>
</input>
```

The definition of the edit form is specified via the **`<form>`** element under the list element. 編集フォームの構造は、入力フォームの構造と同じです。

A **[!UICONTROL Detail]** button is automatically added when the **zoom=&quot;true&quot;** attribute is entered in the list definition. このボタンを使用して、選択した行の編集フォームを開くことができます。

>[!NOTE]
>
>**zoomOnAdd=&quot;true&quot;** 属性を追加すると、リストの要素の挿入時に編集フォームが呼び出されます。

### タブリスト {#tab-list}

タブリストは、コレクション要素をタブ形式で編集できるようにします。

![](assets/d_ncs_content_form6.png)

```
<container toolbarCaption="List of chapters" type="notebooklist" xpath="chapter" xpath-label="@name">
  <container colcount="2">
    <input xpath="@name"/>
    <input xpath="@number"/>
    <input colspan="2" xpath="page"/>
  </container>
</container>
```

このリストコントロールは、**type=&quot;notebooklist&quot;** 属性を使用して設定する必要があります。リストのパスは、コレクション要素を参照する必要があります。

タブのタイトルには、**xpath-label** 属性で入力したデータの値が設定されます。

The edit controls must be declared under a **`<container>`** element that is a child of the list control.

リスト要素を追加または削除するには、ツールバーのボタンを使用します。

>[!NOTE]
>
>左と右の並べ替え矢印は、データスキーマ内のコレクション要素に対して **ordered=&quot;true&quot;** 属性を設定すると、自動的に追加されます。

## コンテナ {#containers}

コンテナを使用すると、一連のコントロールをグループ化できます。They exist via the **`<container>`** element. コンテナは、複数の列でのコントロールの書式設定や、タブリストのコントロール用に、既に使用されています。

コンテナおよび入力フォームでのコンテナの使用方法について詳しくは、[この節](../../configuration/using/form-structure.md#containers)を参照してください。

## フォームの編集 {#editing-forms}

編集領域を使用して、入力フォームの XML コンテンツを入力できます。

![](assets/d_ncs_content_form12.png)

The **[!UICONTROL Preview]** tab lets you view the input form:

![](assets/d_ncs_content_form13.png)
