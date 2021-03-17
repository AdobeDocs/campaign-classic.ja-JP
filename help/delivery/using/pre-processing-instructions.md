---
solution: Campaign Classic
product: campaign
title: トラッキングされる URL の命令の前処理
description: E メールの URL をスクリプト化し、その URL を引き続きトラッキングするための命令の前処理について詳しく説明します。
audience: delivery
content-type: reference
topic-tags: tracking-messages
translation-type: tm+mt
source-git-commit: 8aab4bc23d688aa225cfc636936cf2835840e410
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 65%

---


# 命令の前処理{#pre-processing-instructions}

配信の内容で特定の構文を使用して、手順を追加し、追跡する電子メールのURLをスクリプト化できます。 &lt;%@命令はJavaScriptではありません。この構文はAdobe Campaignに固有です。

&lt;%@ 命令は、配信コンテンツのコンテキストでのみ適用されます。これは、E メールの URL をスクリプト化し、引き続き（URL パラメーター以外を）トラッキングする唯一の方法です。&lt;%@ 命令は、トラッキングするリンクを検出する前の配信分析中に、自動のコピー＆ペーストとして適用されることがあります。

次の 3 種類の命令があります。

* **[!DNL include]**:主に、オプション、パーソナライゼーションブロック、外部ファイル、またはページの一部のコードをファクタリングする場合。[詳細情報](#include)
* **[!DNL value]**:を使用して、配信に読み込まれた配信、配信変数、カスタムオブジェクトのフィールドへのアクセスを許可します。[詳細情報](#value)
* **[!DNL foreach]**:を呼び出します。[詳細情報](#foreach)

配信ウィザードから直接テストできます。これらはコンテンツのプレビューに適用され、トラッキングボタンをクリックすると、URL のリストが表示されます。

## [!DNL include] {#include}

最も一般的に使用される例を次に示します。

* ミラーページリンクを含める：

   ```
   <%@ include view="MirrorPage" %>  
   ```

* ミラーページの URL:

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

   正しい構文を取得するには、配信ウィザードのパーソナライゼーションボタンを使用します。

## [!DNL value] {#value}

この命令は、すべての受信者に対して一定の配信パラメーターに対するアクセスを許可します。

構文：

```
<%@ value object="myObject" xpath="@myField" index="1" %>
```

説明：

* **[!DNL object]**:オブジェクトの名前(例：配信、プロバイダーなど)。オブジェクトは次のいずれかになります。
   * **[!DNL delivery]**:現在の配信について（下記のサブセクションの詳細と制限を参照）。
   * **[!DNL provider]**:現在の配信プロバイダー/ルーティング(nms:externalAccount)の場合。
   * 追加のスクリプトオブジェクト：オブジェクトがコンテキスト内で次から読み込まれる場合：**プロパティ**／**パーソナライゼーション**／**実行コンテキストにオブジェクトを追加**。
   * foreach ループの項目：下の [Foreach](#foreach) の節を参照してください。
* **[!DNL xpath]**:フィールドのxpath。
* **[!DNL index]** （オプション）:が配列 **[!DNL object]** の場合（追加のスクリプトオブジェクトの場合）、配列の項目インデックス(0の開始)。

### [!DNL delivery] object {#delivery-object}

E メールのパーソナライゼーションの場合、配信オブジェクトは次の 2 つの方法でアクセスできます。

* JavaScriptの使用：

   ```
   <%= delivery.myField %>`.
   ```

   JavaScript オブジェクト配信では、カスタムフィールドはサポートされていません。プレビューでは動作しますが、MTA では動作しません（MTA は標準の配信スキーマのみアクセス可能）。

* 前処理の使用：

   ```
   <%@ value object="delivery"
   ```


**注意**

ミッドソーシング経由で送信される配信に次の手順を使用する場合は、マーケティングプラットフォームとミッドソーシングプラットフォームの両方のnms:配信スキーマにカスタムフィールド&#x200B;**@myCustomField**&#x200B;を追加する必要があります。

```
<%@ value object="delivery" xpath="@myCustomField" %>
```

配信パラメーターや配信変数の場合は、次の構文を使用します（配信オブジェクトを使用）。

```
<%@ value object="delivery" xpath="variables/var[@name='myVar']/@stringValue" %>
```

### [!DNL value] JavaScriptセクション内  {#value-in-javascript}

JavaScriptセクションで&lt;%@値を使用できるようにするには、2つの特別なオブジェクトを&lt;%と%>に置き換えます。

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

* **[!DNL object]**:開始元のオブジェクトの名前(通常は追加のスクリプトオブジェクトですが、配信にすることもできます)。
* **[!DNL xpath]** （オプション）:ループ処理を行うコレクションのxpath。初期設定は「.」で、ループする配列がオブジェクトという意味です。
* **[!DNL index]** （オプション）:xpathが「。」でない場合は、「。」オブジェクトが配列自体の場合の、オブジェクトの項目インデックス（0 から開始）。
* **[!DNL item]** （オプション）:アクセス可能な新しいオブジェクトの名前  &lt;>初期設定は、スキーマ内のリンク名です。

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

