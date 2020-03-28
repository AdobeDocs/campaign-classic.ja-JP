---
title: データスキーマ
seo-title: データスキーマ
description: データスキーマ
seo-description: null
page-status-flag: never-activated
uuid: 3327a38c-e44d-4581-a67b-bb60c1604a5f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: aeaa9475-3715-40a4-8864-29d126883272
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# データスキーマ{#data-schemas}

Adobe Campaign のデータスキーマ使用に関する一般的な原理を一部紹介します。

Adobe Campaign でのデータスキーマの作成と設定について詳しくは、[この節](../../configuration/using/about-schema-edition.md)を参照してください。

## スキーマの構造 {#schema-structure}

データスキーマの XML ドキュメントには、**name** 属性と **namespace** 属性が設定された **`<srcschema>`** ルート要素が必要です。これにより、スキーマの名前と名前空間が指定されます。

```
<srcSchema name="schema_name" namespace="namespace">
...
</srcSchema>
```

スキーマのエントリポイントは、スキーマのメイン要素です。メイン要素はスキーマと同じ名前なので、識別は容易です。また、メイン要素はルート要素の子でなければなりません。コンテンツの記述は、この要素から始まります。

コンテンツ管理スキーマでは、メイン要素は次の行で表されます。

```
<element name="book" template="ncm:content" xmlChildren="true">
```

**template** 属性をメイン要素に入力することで、汎用プロパティを持つスキーマを、名前、作成日、作成者、関連付けられた文字列などすべてのコンテンツ定義に拡張できます。

これらのプロパティは、**ncm:content** スキーマに記述します。

>[!NOTE]
>
>**xmlChildren** 属性が存在する場合、メイン要素に入力するデータ構造がコンテンツインスタンスの XML ドキュメントに保存されるということを意味します。

>[!CAUTION]
>
>新しいスキーマを作成するときや、スキーマ拡張の際には、スキーマ全体で同じプライマリキーシーケンス値（@pkSequence）を維持する必要があります。

## データタイプ {#data-types}

タイプが設定されたコンテンツ管理スキーマの例を次に示します。

```
<srcSchema name="book" namespace="cus">
  <element name="book" template="ncm:content" xmlChildren="true">
    <attribute name="title" type="string"/>
    <attribute name="date" type="date"/>
    <attribute name="language" type="string"/>
    <element name="chapter">
      <attribute name="name" type="string"/>
      <element name="page" type="string>
        <attribute name="number" type="short"/>
      </element>
    </element>
  </element>
</element>
```

## プロパティ {#properties}

様々なプロパティを使用して、データスキーマの **`<element>`** 要素と **`<attribute>`** 要素をエンリッチメントできます。

コンテンツ管理で使用する主なプロパティには次のものがあります。

* **label**：短い説明
* **desc**：長い説明
* **default**：コンテンツ作成のデフォルト値を返す式
* **userEnum**：このフィールドに入力された値を保存および表示するための自由列挙
* **enum**：使用可能な値のリストがあらかじめわかっている場合に使用する固定列挙

プロパティが設定されたスキーマの例を次に示します。

```
<srcSchema name="book" namespace="cus">
  <enumeration name="language" basetype="string" default="eng">    
    <value name="fra" label="French"/>    
    <value name="eng" label="English"/>   
  </enumeration>

  <element name="book" label="Book" desc="Example book" template="ncm:content" xmlChildren="true">
    <attribute name="title" type="string" label="Title" default="'New book'"/>
    <attribute name="date" type="date" default="GetDate()"/>
    <attribute name="language" type="string" label="Language" enum="language"/>
    <element name="chapter" label="Chapter">
      <attribute name="name" type="string" label="Name" desc="Name of chapter"/>
      <element name="page" type="string" label="Page" desc="Page content">
        <attribute name="number" type="short" label="Number" default="CounterValue('numPage')"/>
      </element>
    </element>
  </element>
</srcSchema>
```

## コレクション要素 {#collection-elements}

コレクションは、同じ名前と同じ階層レベルを持つ要素のリストです。

次の例では、**`<chapter>`** 要素と **`<page>`** 要素がコレクション要素です。したがって、**unbound** 属性をこれらの要素の定義に追加する必要があります。

```
<element name="chapter" label="Chapter" unbound="true" ordered="true">
```

```
<element name="page" type="string" label="Page" desc="Content of page" unbound="true">
```

>[!NOTE]
>
>**ordered=&quot;true&quot;** 属性を指定することによって、挿入されるコレクション要素を並べ替えることができます。

## 要素の参照 {#element-referencing}

コンテンツスキーマでは、要素の参照が多用されます。これにより、同じ構造を持つ他の要素でも参照できるように、**`<element>`** 要素の定義を分解できます。

参照先要素の **ref** 属性には、参照元要素のパス（XPath）を設定する必要があります。

**例**：サンプルのスキーマの **`<chapter>`** 要素と同じ構造を持つ **Appendix** 節の追加。

```
<srcSchema name="book" namespace="cus">
  <element name="section">
    <attribute name="name" type="string" label="Name" desc="Name"/>
    <element name="page" type="string" label="Page" desc="Content of page">
      <attribute name="number" type="short" label="Number" default="CounterValue('numPage')"/>
    </element>

  <element name="book" label="Book" desc="Example book" template="ncm:content" xmlChildren="true">
    <attribute name="title" type="string" label="Title" default="'New book'"/>
    <attribute name="date" type="date" default="GetDate()"/>
    <attribute name="language" type="string" label="Language" enum="language"/>
    <element name="chapter" label="Chapter" ref="section"/>
    <element name="appendix" label="Appendix" ref="section"/>
  </element>
</srcSchema>
```

chapter の構造は、メイン要素の外側にある「section」という名前の要素に移されます。chapter と section は、「section」要素を参照します。

## 計算文字列 {#compute-string}

**計算文字列**&#x200B;は、コンテンツインスタンスを表す文字列を構成するのに使用する XPath 式です。

**計算文字列**&#x200B;が設定されたスキーマの例を次に示します。

```
<srcSchema name="book" namespace="cus">
  <element name="book" label="Book" desc="Example book" template="ncm:content" xmlChildren="true">
    <compute-string expr="@name"/>
    ...
  </element>
</srcSchema>
```

## スキーマの編集 {#editing-schemas}

編集フィールドを使用して、ソーススキーマの XML コンテンツを入力できます。

![](assets/d_ncs_integration_schema_edition.png)

ソーススキーマを保存すると、拡張スキーマ生成が自動的に開始されます。

>[!NOTE]
>
>「**名前**」編集コントロールを使用して、名前と名前空間で構成されるスキーマのキーを入力できます。スキーマのルート要素の **name** 属性と **namespace** 属性が、スキーマの XML 編集フィールドで自動的に更新されます。
