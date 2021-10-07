---
product: campaign
title: サイトへのタグの挿入
description: サイトへのタグの挿入
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: e7fcec75-82fe-45ff-8d45-7d6e95baeb14
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 5%

---

# サイトへのタグの挿入{#inserting-tags-in-your-site}

![](../../assets/v7-only.svg)

## 簡単な方法 {#simple-method}

このメソッドは、追跡する Web ページのHTMLソースコードに **`<img>`** HTMLタグを挿入することで、リダイレクトサーバーに HTTP 呼び出しを送信する方法です。

>[!IMPORTANT]
>
>この方法では、Web ブラウザーから送信された Cookie を使用して受信者を識別しますが、100%の信頼性はありません。

**例**：

```
<img height='0' width='0' alt='' src='https://localhost/r/12343?tagid=home'
```

挿入されたタグは、リダイレクションサーバーに接続します。

![](assets/d_ncs_integration_webtracking_structure2.png)

コンソールで追跡するページを定義する際に、サンプルの Web トラッキングタグを生成して、コピーし、Web ページのソースコードに貼り付けることができます。

ただし、TRANSACTION タイプのタグを使用する場合は、トランザクション情報（量、項目数）と拡張機能スキーマで定義された情報を挿入するために、JavaScript を使用してサンプルタグを変更する必要があります。

### タグの静的挿入 {#static-insertion-of-tags}

静的タグの挿入を実行するには、コンソールで生成されたタグをコピーして貼り付けるか、手動で作成したタグを Web ページのソースに貼り付けます。

**例**:フォームを表示するページへの web トラッキングタグの挿入

```
<html>
  <...>
  <body>
  <script>
      document.write("<img height='0' width='0' alt='' src='https://localhost/r/" + Math.random().toString() + "?tagid=home'>");
    </script>
    <noscript>
     <img height='0' width='0' alt='' src='https://localhost/r/?tagid=home'>
    </noscript>
    <h1>My site</h1>
    <form action="http://localhost/amount.md">
      Quantity: <input type="text" name="quantity"/><br/><br/>
      Amount: <input type="text" name="amount"/><br/><br/>
      <input value="Save" type="submit">
    </form>
  </body>
</html>
```

確認ページ (「amount.md」) に TRANSACTION タイプの Web トラッキングタグを挿入する。

```
<html>
  <body>
    <script>
      function getURLparam(name) 
      {
        var m = location.search.match new RegExp("[?&]" + name + "=([^&]+)"));
        return m ? unescape(m[1]) : "";
      }
 
       var params = "https://localhost/r/" + Math.random().toString() + "?tagid=amount&amount="
                      +getURLparam("amount")+"&article="+getURLparam("quantity");
       document.write("<img height='0' width='0' src='"+params+"'/>");
    </script>

    <h1>Approval confirmation</h1>
  </body>
</html>
```

### Web トラッキングタグの動的生成 {#dynamic-generation-of-web-tracking-tags}

Web ページが動的に生成される場合は、ページ生成時に Web トラッキングタグを追加できます。

**例**:JSP に追加された Web トラッキング。

```
<%@page import="java.util.Random" %>
<html>
  <body>
    <img height='0' width='0' alt='' src='https://localhost/r/<%=new Random().nextInt()%>?tagid=home'>
    <h1>My site</h1>
    <form action="https://localhost/amount.md">
      Quantity: <input type="text" name="quantity"/><br/><br/>
      Amount: <input type="text" name="amount"/><br/><br/>
      <input value="Save" type="submit">
    </form>
  </body>
</html>
```

```
<%@page import="java.util.Random" %>
<html>
  <body>
    <%  
      String strParams = new Random().nextInt() + "?tagid=amount";
      strParams += "&amount="+request.getParameter("amount");
      strParams += "&article="+request.getParameter("quantity");
    %>
    <img height='0' width='0' alt=''
     src='http://localhost/r/<%=strParams%>'>
    <h1>Approval confirmation</h1>
    </body>
</html>
```

## 最適方法 {#optimum-method-}

リダイレクトサーバーに送信される情報を制御する場合、最も信頼性の高い方法は、ページ生成言語を使用して HTTP クエリを同期的に実行することです。

作成する URL は、[Web トラッキングタグで定義された構文ルールに従う必要があります。定義 ](../../configuration/using/web-tracking-tag--definition.md)。

![](assets/d_ncs_integration_webtracking_structure3.png)

>[!NOTE]
>
>リダイレクトと Web トラッキングでは cookie を使用します。同期 HTTP 呼び出しを実行する Web サーバーは、リダイレクトサーバーと同じドメインに置くことが重要です。 様々な HTTP 交換が、「id」、「uuid」および「uuid230」の Cookie を伝える必要があります。

**例**:Java での動的な生成（アカウント番号を使用した受信者認証）。

```
[...]
  // Recipient account, amount and articles
  String strAccount = request.getParameter("account");
  String strAmount = request.getParameter("amount");
  String strArticle = request.getParameter("article");

  StringBuffer strCookies = new StringBuffer();
  String strSetCookie = null;

  // Get cookies from client request
  Cookie[] cookies = request.getCookies();
  for(int i=0; i< cookies.length; i++ )
  {
    Cookie c = cookies[i];
    String strName = c.getName();
    if( strName.equals("id") || strName.equals("uuid") || strName.equals("uuid230") )
      // Helper function to add cookies in string
      AddCookie(strCookies, c);
  }
  // Now perform a synchronous HTTP request to inform redirection server
  // Add a tagid in auto-discover mode, and a default jobId to use (in hexa)
  StringBuffer strURL = new StringBuffer("https://www.adobe.com/r/a?tagid=cmd_page%7Ct&jobid=27EE");
  if( strAccount != null )
    AddParameter(strURL, "rcpid", "saccount="+strAccount);
  if( strAmount != null )
    AddParameter(strURL, "amount", strAmount);
  if( strArticle != null )
    AddParameter(strURL, "article", strArticle);
  
  URL url = new URL(strURL.toString());
  HttpURLConnection connection = (HttpURLConnection)url.openConnection();
  // Add the client cookies
  if( strCookies.length() > 0 )
    connection.setRequestProperty("Cookie", strCookies.toString());

  int errcode = connection.getResponseCode();

  // Now add the Adobe Campaign cookies if the server returned one :
  if( errcode == 200 )
  {
    strSetCookie = connection.getHeaderField("Set-Cookie");
    if( strSetCookie != null && strSetCookie.length() > 0 )
      response.addHeader("Set-Cookie", strSetCookie);
  }
  [...]
```
