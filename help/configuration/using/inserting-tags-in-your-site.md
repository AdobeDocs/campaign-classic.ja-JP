---
product: campaign
title: サイトに Web トラッキングタグを挿入します。
description: サイトに Web トラッキングタグを挿入する方法を説明します。
feature: Configuration
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: e7fcec75-82fe-45ff-8d45-7d6e95baeb14
source-git-commit: 668cee663890fafe27f86f2afd3752f7e2ab347a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---

# サイトに Web トラッキングタグを挿入します。{#inserting-tags-in-your-site}

## 単純な方法 {#simple-method}

このメソッドは、 **`<img>`** HTMLタグを使用します。

>[!IMPORTANT]
>
>この方法では、Web ブラウザーから送信された Cookie を使用して受信者を識別しますが、100%信頼できるわけではありません。

**例**：

```
<img height='0' width='0' alt='' src='https://localhost/r/12343?tagid=home'
```

挿入されたタグがリダイレクションサーバーに接続します。

![](assets/d_ncs_integration_webtracking_structure2.png)

コンソールで追跡するページを定義する際に、サンプルの Web トラッキングタグを生成して、コピーし、Web ページのソースコードに貼り付けることができます。

ただし、TRANSACTION タイプのタグを使用する場合、トランザクション情報（量、項目数）と、拡張スキーマで定義された情報を挿入するために、JavaScript を使用してサンプルタグを変更する必要があります。

### タグの静的挿入 {#static-insertion-of-tags}

静的タグの挿入を実行するには、コンソールで生成されたタグをコピーして貼り付けるか、手動で作成したタグを Web ページのソースに貼り付けます。

**例**：フォームを表示しているページへの web トラッキングタグの挿入。

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

確認ページ (「amount.md」) への TRANSACTION タイプの Web トラッキングタグの挿入。

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

Web ページが動的に生成される場合、ページ生成時に Web トラッキングタグを追加できます。

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

## 最適な方法 {#optimum-method-}

リダイレクトサーバーに送信される情報を制御する場合、最も信頼性の高い方法は、ページ生成言語を使用して HTTP クエリを同期的に実行することです。

作成する URL は、 [Web トラッキングタグ：定義](../../configuration/using/web-tracking-tag-definition.md).

![](assets/d_ncs_integration_webtracking_structure3.png)

>[!NOTE]
>
>リダイレクションと Web トラッキングでは cookie を使用します。同期 HTTP 呼び出しを実行する Web サーバーが、リダイレクションサーバーと同じドメインにあることが重要です。 様々な HTTP 交換では、「id」、「uuid」および「uuid230」Cookie を伝える必要があります。

**例**:Java での動的生成。受信者認証にアカウント番号を使用します。

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
