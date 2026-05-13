---
product: campaign
title: SOAP を使用した統合（サーバーサイド）
description: SOAP を使用した統合（サーバーサイド）
feature: Interaction, Offers
audience: interaction
content-type: reference
topic-tags: unitary-interactions
exl-id: 3eaef689-44fa-41b3-ade8-9fe447e165ec
TQID: https://experienceleague.adobe.com/-f0NEfvLKh0PfgkB-c4SiPUyQrGuKx55yXOBfmYMmHs
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 326
ht-degree: 81%

---

# SOAP を使用した統合（サーバー側）{#integration-via-soap-server-side}



オファー管理のために用意されている SOAP web サービスは、Adobe Campaign で通常使用されるものとは異なります。 前の節で説明したインタラクション URL でアクセスして、特定のコンタクト先に対するオファーを提示または更新できます。

## オファーの提案 {#offer-proposition}

SOAPを使用したオファー提案の場合、**nms:proposition#Propose** コマンドの後に次のパラメーターを追加します。

* **targetId**：受信者のプライマリキー（複合キーも使用可能）。
* **maxCount**：そのコンタクト先に対するオファーの提案の数を指定します。
* **context**：スペーススキーマにコンテキスト情報を追加できます。 使用するスキーマが&#x200B;**nms:interaction**&#x200B;の場合、**`<empty>`**&#x200B;を追加する必要があります。
* **categories**：オファーが属する必要があるカテゴリを指定します。
* **themes**：オファーが属する必要があるテーマを指定します。
* **uuid**：Adobe Campaign の永続 Cookie の値です（&quot;uuid230&quot;）。
* **nli**：Adobe Campaign のセッション Cookie の値です（&quot;nlid&quot;）。
* **noProp**：値「true」を使用すると、提案の挿入が無効化されます。

>[!NOTE]
>
>**targetId** および **maxCount** の指定は必須です。 その他のパラメーターはオプションです。

クエリに対するの応答では、SOAP サービスは、次のパラメーターを返します。

* **interactionId**：インタラクションの ID。
* **propositions**：提案のリストを含む XML 要素。それぞれに提案自体の ID と HTML 表現が含まれます。

## オファーの更新 {#offer-update}

**nms:interaction#UpdateStatus** コマンドをURLに追加し、次のパラメーターを指定します。

* **proposition**：文字列。オファー提案中の出力として取得した提案 ID が含まれます。 [オファーの提案](#offer-proposition)を参照してください。
* **status**：文字列。オファーの新しいステータスを指定します。 使用可能な値は、**nms:common** スキーマの&#x200B;**propositionStatus**&#x200B;列挙に一覧表示されます。 例えば、デフォルトでは、数字の 3 が&#x200B;**許可済み**&#x200B;ステータスに対応します。
* **context**：XML 要素。スペーススキーマにコンテキスト情報を追加できます。 使用するスキーマが&#x200B;**nms:interaction**&#x200B;の場合、**`<empty>`**&#x200B;を追加する必要があります。

## SOAP 呼び出しの使用例 {#example-using-a-soap-call}

SOAP 呼び出しのコードの例を次に示します。

URL の例を次に示します。

```
http://<urlOfYourJSSP>?env=liveRcp&sp=<nameSpaceOfferSpace>&t=<targetID>
```

```
<%
  var env = request.getUTF8Parameter("env");
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
      for each( var propHtml in props.proposition.*.htmlSource )
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
