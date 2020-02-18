---
title: サイトへのタグの挿入
seo-title: サイトへのタグの挿入
description: サイトへのタグの挿入
seo-description: null
page-status-flag: never-activated
uuid: e5e4a431-2093-4d5a-acd2-0040b6ce3519
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 57988b00-62cc-43d3-a2eb-bfed5bff7dc1
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# サイトへのタグの挿入{#inserting-tags-in-your-site}

## 簡単な方法 {#simple-method}

このメソッドは、追跡するWebページのHTMLソースコードに **`<img>`** HTMLタグを挿入することによって、リダイレクトサーバーにHTTP呼び出しを送信することから構成されます。

>[!IMPORTANT]
>
>この方法では、Webブラウザーから送信されたcookieを使用して受信者を識別しますが、信頼性は100 %ではありません。

**例**：

```
<img height='0' width='0' alt='' src='https://localhost/r/12343?tagid=home'
```

挿入されたタグがリダイレクトサーバーに接続します。

![](assets/d_ncs_integration_webtracking_structure2.png)

コンソールで追跡するページを定義する際に、サンプルのWebトラッキングタグを生成して、Webページのソースコードにコピー&amp;ペーストできます。

ただし、TRANSACTIONタイプのタグを使用する場合は、トランザクション情報（金額、項目数）と拡張スキーマで定義された情報を挿入するために、JavaScriptを使用してサンプルタグを変更する必要があります。

### タグの静的挿入 {#static-insertion-of-tags}

静的タグの挿入を実行するには、コンソールで生成されたタグをコピーして貼り付けるか、Webページのソースに手動で作成したタグを貼り付けます。

**例**:フォームを表示するページへのWebトラッキングタグの挿入。

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

確認ページ(「amount.md」)へのTRANSACTIONタイプのWebトラッキングタグの挿入。

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

### Webトラッキングタグの動的生成 {#dynamic-generation-of-web-tracking-tags}

Webページが動的に生成される場合、ページ生成時にWebトラッキングタグを追加できます。

**例**:JSPに追加されたWebトラッキング。

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

## 最適な方法 {#optimum-method-}

リダイレクトサーバーに送信される情報を制御する場合、最も信頼性の高い方法は、ページ生成言語を使用して自身で同期的にHTTPクエリを実行することです。

構築するURLは、 [Webトラッキングタグで定義されている構文ルールに従う必要があります。定義](../../configuration/using/web-tracking-tag--definition.md)。

![](assets/d_ncs_integration_webtracking_structure3.png)

>[!NOTE]
>
>リダイレクトとWebトラッキングではcookieを使用します。同期HTTP呼び出しを実行するWebサーバーは、リダイレクトサーバーと同じドメインに配置することが重要です。 様々なHTTP交換では、「id」、「uuid」および「uuid230」の各cookieを伝える必要があります。

**例**:アカウント番号を使用した受信者認証を使用したJavaでの動的生成。

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

