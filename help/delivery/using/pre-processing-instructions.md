---
solution: Campaign Classic
product: campaign
title: 追跡するURLの前処理手順
description: 電子メールのURLのスクリプトを作成し、そのURLを引き続き追跡するために使用する事前処理の手順について詳しく説明します。
audience: delivery
content-type: reference
topic-tags: tracking-messages
translation-type: tm+mt
source-git-commit: 3454af2faffacd43fa1ad852529dad175340a237
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# 前処理命令{#pre-processing-instructions}

&lt;%@命令はJavaScriptではなく、Adobe Campaignに固有の構文です。

これらは、配信コンテンツのコンテキストにのみ適用されます。 電子メールのURLをスクリプトし、引き続き（URLパラメーター以外）追跡する唯一の方法です。 これは、トラッキングするリンクを検出する前に配信分析中に適用される自動コピー/貼り付けと見なすことができます。

手順には次の3種類があります。

* &quot;**include**&quot;:主にオプション、パーソナライゼーションブロック、外部ファイル、またはページの一部のコードをファクタリングする
* &quot;**値**&quot;:配信に読み込まれた配信、配信変数、カスタムオブジェクトのフィールドへのアクセスを許可するには
* &quot;**foreach**&quot;:を呼び出します。

配信ウィザードから直接テストできます。 これらの指標はコンテンツプレビューに適用され、追跡ボタンをクリックしてURLのリストを表示します。

## &lt;>{#include}

最も一般的に使用される例を次に示します。

* ミラーページリンクを含める：`<%@ include view="MirrorPage" %>`
* ミラーページURL:&quot;`<a href="<%@ include view='MirrorPageUrl' %>" _label="Mirror Page" _type="mirrorPage">web page"`としての表示
* 標準搭載の購読解除URL:`<%@ include option='NmsServer_URL' %>/webApp/unsub?id=<%= escapeUrl(recipient.cryptedId)%>`
* その他の例：
   * `<%@ include file='http://www.google.com' %>`
   * `<%@ include file='file:///X:/france/service/test.html' %>`
   * `<%@ include option='NmsServer_URL' %>`

正しい構文を取得するには、配信ウィザードのパーソナライゼーションボタンを使用します。

## &lt;%@ value {#value}

この命令は、すべての受信者に対して定数の配信のパラメータにアクセスを与えます。

構文:

`<%@ value object="myObject" xpath="@myField" index="1" %>`

場所：

* &quot;object&quot;:オブジェクトの名前(例：配信、プロバイダーなど)。
* &quot;xpath&quot;:フィールドのxpath。
* &quot;index&quot;（オプション）:&quot;object&quot;が配列（追加のスクリプトオブジェクトの場合）の場合、配列内の項目インデックス(0の開始)。

オブジェクトは次のいずれかになります。

* &quot;配信&quot;:現在の配信について（下記のサブセクションの詳細と制限を参照）。
* &quot;provider&quot;:現在の配信プロバイダー/ルーティング(nms:externalAccount)の場合。
* 追加のスクリプトオブジェクト：オブジェクトがコンテキスト内で次を通して読み込まれる場合：**プロパティ** > **パーソナライゼーション** > **追加実行コンテキスト**&#x200B;のオブジェクト。
* foreachループの項目：[下の](#foreach)セクションを参照してください。

### &quot;配信&quot;オブジェクト{#delivery-object}

電子メールのパーソナライゼーションの場合、配信オブジェクトには次の2つの方法でアクセスできます。

* JavaScriptの場合。 例：`<%= delivery.myField %>`

   JavaScriptオブジェクト配信では、カスタムフィールドはサポートされていません。 MTAはプレビューで動作しますが、MTAでは動作しません。MTAは、標準搭載された配信スキーマにしかアクセスできないからです。

* `<%@ value object="delivery"`前処理を通じて。

`<%@ value object="delivery" xpath="@myCustomField" %>`命令には、ミッドソーシングを介して送信される配信には別の制限があります。 マーケティングプラットフォームとミッドソーシングプラットフォームの両方で、カスタムフィールド@myCustomFieldをnms:配信スキーマに追加する必要があります。

>[!NOTE]
>
>配信パラメーター/変数の場合は、次の構文を使用します(配信オブジェクトの使用)。
>
>`<%@ value object="delivery" xpath="variables/var[@name='myVar']/@stringValue" %>`

### &lt;>{#value-in-javascript}

スクリプトセクションで&lt;%@値を使用できるようにするには、2つの特別なオブジェクトを&lt;%と%>に置き換えます。

* `<%@ value object='startScript' %>`
* `<%@ value object='endScript' %>`

例：

```
<%@ value object='startScript' %> var iMode = <%@ value object="delivery" xpath="@deliveryMode" %> if(iMode == 1) { ... } else { ... }`
`<%@ value object='endScript' %> is expanded in something like <% var iMode = 1 if(iMode == 1) { ... } else { ... } %>.
```

## &lt;>{#foreach}

この命令は、配信にロードされたオブジェクトの配列の反復を可能にし、オブジェクトに関連する個々のリンクを追跡します。

構文:

`<%@ foreach object="myObject" xpath="myLink" index="3" item="myItem" %> <%@ end %>`

場所：

* &quot;object&quot;:開始元のオブジェクトの名前(通常は追加のスクリプトオブジェクトですが、配信にすることもできます)。
* &quot;xpath&quot;（オプション）:ループ処理を行うコレクションのxpath。 初期設定は「。」で、ループする配列がオブジェクトです。
* &quot;index&quot;（オプション）:xpathが「。」でない場合は、「。」 とobjectは配列自体、オブジェクトの項目インデックス(0の開始)です。
* &quot;item&quot;（オプション）:foreachループ内に&lt;%@値を指定してアクセスできる新しいオブジェクトの名前。 初期設定は、スキーマ内のリンク名です。

例：

配信のプロパティ/パーソナライゼーションで、受信者の配列と記事と記事と記事との関係テーブルを読み込みます。

これらの記事へのリンクの表示は、次のようにJavaScriptを使用して行うだけで済みます。

```
<%
  for(var i=0; i<recipient.rcpArticle.length; i++ )
  {
    %><a href="http://nl.net?a.jsp?article=<%=recipient.rcpArticle[i].article.@id%>">article</a><%
  }
%>
```

このソリューションでは、すべての記事へのリンクが区別なく追跡されます。 受信者が記事のリンクをクリックしたことはわかりますが、どの記事かはわかりません。

解決策は次のとおりです。

1. 可能なすべての記事を、配信articleList[]の追加のスクリプト配列(articleList)で事前に読み込みます。これは、可能な記事の数が有限である必要があることを意味します。
1. コンテンツの先頭にJavaScript関数を記述します。

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

