---
title: コンテンツのエンリッチメント
seo-title: コンテンツのエンリッチメント
description: コンテンツのエンリッチメント
seo-description: null
page-status-flag: never-activated
uuid: 6f1bce9f-88ed-4ad3-987f-79f6c68264d2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: 4404c21e-0a89-4762-af20-384ad7071916
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# コンテンツのエンリッチメント{#enriching-content}

集約機能を利用すると、コンテンツを外部データでエンリッチメントできます。このデータは、汎用クエリまたはリンクされたテーブルから取得します。

## 汎用クエリ {#generic-queries}

クエリは、「**[!UICONTROL 集約]**」タブでパブリッシュテンプレートを使用して設定します。

XML 出力ドキュメントのメイン要素を使用して、取得したデータでこのドキュメントをエンリッチメントします。

受信者スキーマ（**nms:recipient**）に対するクエリの戻り値の例：

```
<book name="Content Management">
  ...
  <collection-recipient>
    <recipient lastName="Doe" firstName="John" email="john.doe@aolf.com">
    ...
  </collection-recipient>
</book>
```

**`<collection-recipient>`** 要素は、クエリ結果のドキュメントの入力要素を表します。取得したデータは、この要素の下に返されます（この例では受信者リスト）。

### クエリの追加 {#adding-a-query}

クエリのパラメーターは、ウィザードを使用して編集します。

1. 最初のページで、ラベルおよび取得するデータを含むスキーマを指定します。

   ![](assets/d_ncs_content_query1.png)

   >[!NOTE]
   >
   >「**パス**」編集フィールドを使用して、クエリの出力要素名を変更します。

1. 次のページでは、取得するデータを選択できます。

   ![](assets/d_ncs_content_query2.png)

1. 次のページでは、フィルター条件を定義します。

   ![](assets/d_ncs_content_query3.png)

1. 最後のページで、クエリが返すデータのプレビューを開始します。

   ![](assets/d_ncs_content_query4.png)

## リンクされたテーブル {#linked-tables}

リンクを使用して、コンテンツにリンクされた外部データを取得できます。

次の 2 種類のリンク済みデータがあります。

* コンテンツリンク：ネイティブなコンテンツ管理モードです。リンクのコンテンツは、XML 出力ドキュメントに自動的に統合されます。
* 外部テーブルへのリンクによって、データベース内のその他すべてのテーブルにアクセスできます。その際、選択したリンクのデータを集約で取得するという制約があります。

### コンテンツスキーマへのリンク {#link-to-a-content-schema}

コンテンツリンクは、データスキーマ内で次のように宣言します。

```
<element expandSchemaTarget="cus:chapter" label="Main chapter" name="mainChapter" type="string"/>
```

リンクの定義は **string** タイプの **`<element>`** に対して設定され、**expandSchemaTarget** 属性がターゲットスキーマ（この例では「cus:chapter」）を参照します。参照するスキーマは、コンテンツスキーマである必要があります。

ターゲット要素のコンテンツは、リンク要素（この例のスキーマでは **`<chapter>`** 要素）をエンリッチメントします。

```
<mainChapter computeString="Introduction" id="7011" title="Introduction" xtkschema="cus:chapter">    
  <page>Introduction to input <STRONG>forms</STRONG>.</page>
</mainChapter>
```

>[!NOTE]
>
>リンクの&#x200B;**計算文字列**&#x200B;は、**computeString** 属性から提供されます。

リンクの編集コントロールは、入力フォーム内で次のように宣言します。

```
<input type="articleEdit" xpath="mainChapter"/>
```

![](assets/d_ncs_content_link.png)

**[!UICONTROL 虫眼鏡]**&#x200B;アイコンを使用して、リンクされている要素の編集フォームを開くことができます。

#### リンクコレクション {#link-collection}

リンクのコレクションを設定するには、データスキーマ内のリンク要素の定義に **unbound=&quot;true&quot;** 属性を追加します。

```
<element expandSchemaTarget="cus:chapter" label="List of chapters" name="chapter"  ordered="true" unbound="true"/>
```

ターゲット要素のコンテンツは、各コレクション要素をエンリッチメントします。

```
<chapter computeString="Introduction" id="7011" title="Introduction" xtkschema="cus:chapter">    
  <page>Introduction to input <STRONG>forms</STRONG>.</page>
</chapter>
```

リストコントロールは、入力フォーム内で次のように宣言します。

```
<input editable="false" nolabel="true" toolbarCaption="List of chapters" type="articleList" xpath="chapter" zoom="true"/>
```

![](assets/d_ncs_content_link2.png)

ターゲット要素の&#x200B;**計算文字列**&#x200B;を確認するために、デフォルトの列が表示されます。

### 外部テーブルへのリンク {#links-to-external-tables}

外部テーブルへのリンクは、データスキーマ内で次のように宣言します。

```
<element label="Main contact" name="mainContact" target="nms:recipient" type="link"/>
```

リンクの定義は **link** タイプの **`<element>`** に対して設定され、**target** 属性がターゲットスキーマ（この例では「nms:recipient」）を参照します。

慣例によって、リンクはデータスキーマのメイン要素から宣言する必要があります。

ターゲット要素の&#x200B;**計算文字列**&#x200B;とキーが、メイン要素の **`<name>-id`** 属性と **`<name>-cs`** 属性をエンリッチメントします。

この例では、リンクは「cus:book」スキーマ内に入力され、リンクデータのコンテンツは「mainContact-id」属性と「mainContact-cs」属性に格納されます。

```
<book computeString="Content management" date="2006/06/08" id="6106" language="en" mainContact-cs="John Doe (john.doe@adobe.com)" mainContact-id="3012" name="Content management" xtkschema="cus:book">
```

リンク編集コントロールは次のように宣言します。

```
<input xpath="mainContact"/>
```

![](assets/d_ncs_content_link3.png)

入力フォーム内のリンク定義を使用して **`<sysfilter>`** 要素を追加することによって、ターゲット要素の選択肢を制限できます。

```
<input xpath="mainContact">
  <!-- Filter the selection of the link on the Adobe domain -->
  <sysFilter>
    <condition expr="@domain =  'adobe.com '"/>
  </sysFilter>
</input>
```

>[!NOTE]
>
>この制約はコンテンツリンクにも適用されます。

#### リンクコレクション {#link-collection-1}

コレクションの定義は、コレクション要素に対するリストの定義と同じです。

```
<element label="List of contacts" name="contact" unbound="true">
  <element label="Recipient" name="recipient" target="nms:recipient" type="link"/>
</element>
```

リストコントロールは、入力フォーム内で次のように宣言します。

```
<input nolabel="true" toolbarCaption="List of contacts" type="list" xpath="contact">
  <input xpath="recipient"/>
</input>
```

![](assets/d_ncs_content_link4.png)

>[!NOTE]
>
>リストは編集可能で、上述の「リンク」タイプのコントロールからリンクを選択できます。

ターゲット要素のコンテンツは、出力ドキュメント内の各コレクション要素をエンリッチメントします。

```
<contact id="11504978621" recipient-cs="Doe John (john.doe@adobe.com)" recipient-id="3012"/>
<contact id="11504982510" recipient-cs="Martinez Peter (peter.martinez@adobe.com)" recipient-id="3013"/>
```

#### リンクの集約 {#link-aggregation}

参照される各リンクのコンテンツは、ターゲット要素の内部キーと&#x200B;**計算文字列**&#x200B;に制限があります。

JavaScript スクリプトを使用して、SOAP クエリによってリンクのコンテンツをエンリッチメントします。

**例**：「mainContact」リンクおよび「contact」コレクションリンクに受信者名を追加：

```
// Update <mainContact> link
var mainContactId = content.@['mainContact-id']
var query = xtk.queryDef.create(
    <queryDef schema="nms:recipient" operation="get">
      <select>
        <node expr="@lastName"/>
      </select>
      <where>
        <condition expr={"@id="+mainContactId}/>
      </where>
    </queryDef>)

var recipient = query.ExecuteQuery()
content.mainContact.@lastName = recipient.@lastName

// Update <contact> link collection
for each(var contact in content.contact)
{
  var contactId = contact.@['recipient-id']
  var query = xtk.queryDef.create(
    <queryDef schema="nms:recipient" operation="get">
      <select>
        <node expr="@lastName"/>
      </select>
      <where>
        <condition expr={"@id="+contactId}/>
      </where>
    </queryDef>
  )
  
  var recipient = query.ExecuteQuery()
  contact.@lastName = recipient.@lastName
}
```

スクリプト実行後に取得された結果：

```
<mainContact lastName="Doe"/>

<contact id="11504978621" lastName="Doe" recipient-cs="Doe John (john.doe@adobe.com)" recipient-id="3012"/>  
<contact id="11504982510" lastName="Martinez" recipient-cs="Martinez Peter (peter.martinez@adobe.com)" recipient-id="3013"/> 
```

JavaScript コードのコンテンツが&#x200B;**[!UICONTROL 管理／設定／コンテンツ管理／JavaScript コード]**&#x200B;フォルダーを使用して追加されます。また、コンテンツは変換ごとにパブリッシュテンプレートに追加される必要があります。

![](assets/d_ncs_content_link5.png)

