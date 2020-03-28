---
title: SOAP による統合（サーバー側）
seo-title: SOAP による統合（サーバー側）
description: SOAP による統合（サーバー側）
seo-description: null
page-status-flag: never-activated
uuid: 678371c5-4246-4886-994e-30dbbc70f14a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: unitary-interactions
discoiquuid: 477a2c31-0403-4db1-a372-c75dca58380d
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# SOAP による統合（サーバー側）{#integration-via-soap-server-side}

オファー管理のために用意されている SOAP Web サービスは、Adobe Campaign で通常使用されるものとは異なります。前の節で説明したインタラクション URL でアクセスして、特定のコンタクト先に対するオファーを提示または更新できます。

## オファーの提案 {#offer-proposition}

SOAP によるオファーの提案の場合、**nms:proposition#Propose** コマンドを追加し、その後に次のパラメーターが続きます。

* **targetId**：受信者のプライマリキー（複合キーも使用可能）。
* **maxCount**：そのコンタクト先に対するオファーの提案の数を指定します。
* **context**：スペーススキーマにコンテキスト情報を追加できます。使用されるスキーマが **nms:interaction** の場合、**`<empty>`** を追加する必要があります。
* **categories**：オファーが属する必要があるカテゴリを指定します。
* **themes**：オファーが属する必要があるテーマを指定します。
* **uuid**：Adobe Campaign の永続 Cookie の値です（&quot;uuid230&quot;）。
* **nli**：Adobe Campaign のセッション Cookie の値です（&quot;nlid&quot;）。
* **noProp**：値「true」を使用すると、提案の挿入が無効化されます。

>[!NOTE]
>
>**targetId** および **maxCount** の指定は必須です。その他のパラメーターはオプションです。

クエリに対するの応答では、SOAP サービスは、次のパラメーターを返します。

* **interactionId**：インタラクションの ID。
* **propositions**：提案のリストを含む XML 要素。それぞれに提案自体の ID と HTML 表現が含まれます。

## オファーの更新 {#offer-update}

URL に **nms:interaction#UpdateStatus** コマンドを追加し、その後に次のパラメーターが続きます。

* **proposition**：文字列。オファー提案中の出力として取得した提案 ID が含まれます。[オファーの提案](#offer-proposition)を参照してください。
* **status**：文字列。オファーの新しいステータスを指定します。使用可能な値のリストについては、**nms:common** スキーマの **propositionStatus** 列挙を参照してください。例えば、デフォルトでは、数字の 3 が&#x200B;**許可済み**&#x200B;ステータスに対応します。
* **context**：XML 要素。スペーススキーマにコンテキスト情報を追加できます。使用されるスキーマが **nms:interaction** の場合、**`<empty>`** を追加する必要があります。

## SOAP 呼び出しの使用例 {#example-using-a-soap-call}

SOAP 呼び出しのコードの例を次に示します。

```
<%
  var space = request.parameters.sp
  var cnx = new HttpSoapConnection(
    "https://" + request.serverName + ":" + request.serverPort + "/interaction/" + env + "/" + space,
    "utf-8",
    HttpSoapConnection.SOAP_12)
  var session = new SoapService(cnx, "nms:interaction")
  var action = request.parameters.a
  if( action == undefined )
    action = 'propose'

  try
  {
    switch( action )
    {
    case "update":
      var proposition = request.parameters.p
      var status      = request.parameters.st
      session.addMethod("UpdateStatus", "nms:interaction#UpdateStatus",
       ["proposition", "string",
        "status",      "string",
        "context",     "NLElement"],
       [])
      session.UpdateStatus(proposition, status, <undef/>)
      var redirect = request.parameters.r
      if( redirect != undefined )
        response.sendRedirect(redirect)
      break;

    case "propose":
      var count = request.parameters.n
      var target = request.parameters.t
      var categorie = request.parameters.c
      var theme = request.parameters.th
      var layout = request.parameters.l
      if( count == undefined )
        count = 1
      session.addMethod("Propose", "nms:proposition#Propose",
       ["targetId",      "string",
        "maxCount",      "string",
         "categories",    "string",
         "themes",        "string",
        "context",       "NLElement"],
       ["interactionId", "string",
        "propositions",  "NLElement"])
      response.setContentType("text/html")
      var result = session.Propose(target, count, category, theme, <empty/>)
      var props = result[1]
  %><table><tr><%
      for each( var propHtml in props.proposition.*.mdSource )
      {
        %><td><%=propHtml%></td><%
      }
  %></tr></table><%
      break;
    }
  }
  catch( e )
  {
  }
  %>
```
