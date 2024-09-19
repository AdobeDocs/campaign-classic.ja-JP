---
product: campaign
title: トラッキングされる URL の命令の前処理
description: メールの URL をスクリプト化し、その URL を引き続きトラッキングするための命令の前処理について詳しく説明します。
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Monitoring
role: User, Data Engineer, Developer
exl-id: 9d3f5c74-377a-4e24-81e5-bb605f69cf8a
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: ht
source-wordcount: '653'
ht-degree: 100%

---

# 命令の前処理 {#pre-processing-instructions}

配信コンテンツで特定の構文を使用して、命令を追加し、トラッキングされるメールの URL をスクリプト化できます。 &lt;%@ 命令は JavaScript ではありません。Adobe Campaign 固有の構文です。

&lt;%@ 命令は、配信コンテンツのコンテキストでのみ適用されます。これは、メールの URL をスクリプト化し、引き続き（URL パラメーター以外を）トラッキングする唯一の方法です。&lt;%@ 命令は、トラッキングするリンクを検出する前の配信分析中に、自動のコピー＆ペーストとして適用されることがあります。

次の 3 種類の命令があります。

* **[!DNL include]**：主にオプション、パーソナライゼーションブロック、外部ファイル、ページに含まれる一部のコードを変数化します。[詳細情報](#include)
* **[!DNL value]**：配信のフィールド、配信変数、配信に読み込まれたカスタムオブジェクトにアクセスできるようにします。[詳細情報](#value)
* **[!DNL foreach]**：カスタムオブジェクトとして読み込まれた配列をループ処理します。 [詳細情報](#foreach)

配信アシスタントから直接テストできます。これらはコンテンツのプレビューに適用され、トラッキングボタンをクリックすると、URL のリストが表示されます。

## [!DNL include] {#include}

最も一般的に使用される例を次に示します。

* ミラーページリンクのインクルード：

  ```
  <%@ include view="MirrorPage" %>  
  ```

* ミラーページの URL：

  ```
  View as a <a href="<%@ include view='MirrorPageUrl' %>" _label="Mirror Page" _type="mirrorPage">web page.
  ```

* 標準の購読解除 URL：

  ```
  <%@ include option='NmsServer_URL' %>/webApp/unsub?id=<%= escapeUrl(recipient.cryptedId)%>
  ```

* その他の例：

  ```
  <%@ include file='http://www.google.com' %>
  <%@ include file='file:///X:/france/service/test.html' %>
  <%@ include option='NmsServer_URL' %>
  ```

  正しい構文を取得するには、配信アシスタントのパーソナライゼーションボタンを使用します。

## [!DNL value] {#value}

この命令は、すべての受信者に対して一定の配信パラメーターに対するアクセスを許可します。

構文：

```
<%@ value object="myObject" xpath="@myField" index="1" %>
```

説明：

* **[!DNL object]**：オブジェクト（例：配信、プロバイダーなど）の名前。オブジェクトは次のいずれかになります。
   * **[!DNL delivery]**：現在の配信の場合（詳細と制限事項については下記を参照）。
   * **[!DNL provider]**：現在の配信プロバイダー／ルーティング（nms:externalAccount）の場合。
   * 追加のスクリプトオブジェクト：オブジェクトがコンテキスト内で次から読み込まれる場合：**プロパティ**／**パーソナライゼーション**／**実行コンテキストにオブジェクトを追加**。
   * foreach ループの項目：下の [Foreach](#foreach) の節を参照してください。
* **[!DNL xpath]**：フィールドの xpath。
* **[!DNL index]** （オプション）：**[!DNL object]** が配列（追加のスクリプトオブジェクト向け）の場合、配列内の項目インデックス（0 から開始）。

### [!DNL delivery] オブジェクト{#delivery-object}

メールのパーソナライゼーションの場合、delivery オブジェクトは次の 2 とおりの方法でアクセスできます。

* JavaScript の使用：

  ```
  <%= delivery.myField %>`.
  ```

  JavaScript オブジェクト配信では、カスタムフィールドはサポートされていません。プレビューでは動作しますが、MTA では動作しません（MTA は標準の配信スキーマのみアクセス可能）。

* 前処理の使用：

  ```
  <%@ value object="delivery"
  ```


**注意**

ミッドソーシング経由で送信される配信に次の命令を使用する場合は、マーケティングプラットフォームとミッドソーシングプラットフォームの両方の nms:delivery スキーマにカスタムフィールド **@myCustomField** を追加する必要があります。

```
<%@ value object="delivery" xpath="@myCustomField" %>
```

配信パラメーターや配信変数の場合は、次の構文を使用します（delivery オブジェクトを使用）。

```
<%@ value object="delivery" xpath="variables/var[@name='myVar']/@stringValue" %>
```

### JavaScript セクション内の [!DNL value]  {#value-in-javascript}

JavaScript セクションで &lt;%@ value を使用できるようにするために、次の 2 つの特別なオブジェクトが &lt;% と %> に置き換えられます。

```
<%@ value object='startScript' %>
<%@ value object='endScript' %>
```

例：

```
<%@ value object='startScript' %> var iMode = <%@ value object="delivery" xpath="@deliveryMode" %> if(iMode == 1) { ... } else { ... }`
`<%@ value object='endScript' %> is expanded in something like <% var iMode = 1 if(iMode == 1) { ... } else { ... } %>.
```

## [!DNL foreach] {#foreach}

この命令は、配信に読み込まれたオブジェクトの配列の反復を可能にし、オブジェクトに関連する個々のリンクをトラッキングします。

構文：

```
<%@ foreach object="myObject" xpath="myLink" index="3" item="myItem" %> <%@ end %>
```

説明：

* **[!DNL object]**：開始点となるオブジェクトの名前。通常は追加のスクリプトオブジェクトですが、配信の場合もあります。
* **[!DNL xpath]**（オプション）：ループ処理の対象となるコレクションの xpath。 デフォルトは「.」です。これは、オブジェクトがループ処理の対象となる配列であることを意味します。
* **[!DNL index]**（オプション）：xpath が「.」でなく、オブジェクトが配列そのものである場合は、オブジェクトの項目インデックスです（0 から開始）。
* **[!DNL item]**（オプション）：foreach ループ内で &lt;%@ 値でアクセス可能な新しいオブジェクトの名前。 初期設定は、スキーマ内のリンク名です。

例：

配信プロパティ／パーソナライゼーションで、記事の配列と、受信者と記事のリレーションテーブルを読み込みます。

これらの記事へのリンクの表示は、次のように JavaScript を使用して容易におこなえます。

```
<%
  for(var i=0; i<recipient.rcpArticle.length; i++ )
  {
    %><a href="http://nl.net?a.jsp?article=<%=recipient.rcpArticle[i].article.@id%>">article</a><%
  }
%>
```

この方法では、すべての記事へのリンクが区別なくトラッキングされます。受信者が記事のリンクをクリックしたことはわかりますが、どの記事かはわかりません。

解決策は次のとおりです。

1. 可能なすべての記事を、配信の追加スクリプト配列（articleList[]）で事前に読み込んでおきます。つまり、可能な記事数は有限である必要があります。
1. コンテンツの先頭に JavaScript 関数を記述します。

   ```
   <%@ value object='startScript' %>
   function displayArticle(articleId)
   {
     <%@ foreach object="articleList" item="article" %>
       if( articleId == <% value object="article" xpath="@id" %> ) 
       {
         <%@ value object='endScript' %>
           <a href="http://nl.net?a.jsp?article=<%@ value object="article" xpath="@id" %>">article</a>
         <%@ value object='startScript' %>
       } 
     <%@ end @%>
   }
   <%@ value object='endScript' %>
   ```

1. 関数を呼び出して記事を表示します。

   ```
   <%
   for(var i=0; i<recipient.rcpArticle.length; i++ )
   {
    displayArticle(recipient.rcpArticle[i].article.@id)
   }
   %>
   ```
