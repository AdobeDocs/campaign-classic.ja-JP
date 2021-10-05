---
product: campaign
title: Web サービスについて
description: Web サービスについて
audience: configuration
content-type: reference
topic-tags: api
exl-id: 7aa2aef1-2eb6-48a6-82fa-4451bed66216
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 9%

---

# Web サービスについて{#about-web-services}

![](../../assets/v7-only.svg)

## Adobe Campaign API の定義 {#definition-of-adobe-campaign-apis}

Adobe Campaignアプリケーションサーバは、より多様で複雑な企業情報システムとのオープン性と容易な統合を実現するように設計されています。

Adobe Campaign API は、アプリケーション内の JavaScript と、その外部の SOAP で使用されます。 エンリッチメントできる汎用関数のライブラリを構成しています。 詳しくは、[SOAP メソッドの実装 ](../../configuration/using/implementing-soap-methods.md) を参照してください。

>[!IMPORTANT]
>
>1 日あたりの許可されたエンジン呼び出しの数は、ライセンス契約によって異なります。 詳しくは、[このページ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-classic---product-description.html)を参照してください。\
>すべての API の詳細な説明を含むリストは、[ この専用ドキュメント ](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html) で入手できます。

## 前提条件 {#prerequisites}

Adobe Campaign API を使用する前に、次のトピックに精通しておく必要があります。

* JavaScript
* SOAP プロトコル
* Adobe Campaign データモデル

## Adobe Campaign API の使用 {#using-adobe-campaign-apis}

Adobe Campaignは、次の 2 種類の API を使用します。

* データモデルデータに対してクエリを実行するための汎用データアクセス API。 [データ指向 API](../../configuration/using/data-oriented-apis.md) を参照してください。
* 目的の対象ごとにアクションをおこなえる、ビジネスに特化した API。配信、ワークフロー、サブスクリプションなど。[ ビジネス指向 API](../../configuration/using/business-oriented-apis.md) を参照してください。

API を開発し、Adobe Campaignとやり取りするには、データモデルに精通している必要があります。 Adobe Campaignでは、ベースの完全な説明を生成できます。 [ モデルの説明 ](../../configuration/using/data-oriented-apis.md#description-of-the-model) を参照してください。

## SOAP 呼び出し {#soap-calls}

SOAP プロトコルを使用すると、リッチクライアント、Web サービスを使用するサードパーティアプリケーション、またはこれらのメソッドをネイティブに使用した JSP を介して API メソッドを呼び出すことができます。

![](assets/s_ncs_configuration_architecture.png)

SOAP メッセージの構造を次に示します。

* メッセージの構造を定義する封筒
* オプションのヘッダー
* 呼び出しと応答に関する情報を含む本文
* エラーの管理：エラーの状態を定義します。

## リソースと交換 {#resources-and-exchanges}

次のスキーマは、Adobe Campaign API の使用に関連する様々なリソースを示しています。

![](assets/s_ncs_integration_webservices_schema_pres.png)

## 「ExecuteQuery」メソッドでの SOAP メッセージの例 {#example-of-a-soap-message-on-the--executequery--method--}

この例では、SOAP クエリが「ExecuteQuery」メソッドを呼び出します。このメソッドは、文字列を認証用のパラメーター（セッショントークン）とし、XML コンテンツを取得して実行するクエリの説明を示します。

詳しくは、[ExecuteQuery (xtk:queryDef)](../../configuration/using/data-oriented-apis.md#executequery--xtk-querydef-) を参照してください。

>[!NOTE]
>
>このサービスの WSDL 記述は、次の例に示すように入力されます。[Web サービスの説明：WSDL](../../configuration/using/web-service-calls.md#web-service-description--wsdl)。

### SOAP クエリ {#soap-query}

```
<?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <ExecuteQuery xmlns='urn:xtk:queryDef' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <__sessiontoken xsi:type='xsd:string'/>
        <entity xsi:type='ns:Element' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <queryDef firstRows="true" lineCount="200" operation="select" schema="nms:rcpGrpRel" startLine="0" startPath="/" xtkschema="xtk:queryDef">
          ...
          </queryDef>
        </entity>
      </ExecuteQuery>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

`<soap-env:envelope>` 要素は、SOAP エンベロープを表すメッセージの最初の要素です。

`<soap-env:body>` 要素はエンベロープの最初の子要素です。 メッセージの説明（クエリの内容や応答の内容）が含まれます。

呼び出すメソッドは、SOAP メッセージの本文の `<executequery>` 要素に入力します。

SOAP では、パラメータは出現順に認識されます。 最初のパラメータ `<__sessiontoken>` は認証チェーンを取り、2 番目のパラメータは `<querydef>` 要素からのクエリの XML 記述です。

### SOAP 応答 {#soap-response}

```
<?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <ExecuteQueryResponse xmlns='urn:xtk:queryDef' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <pdomOutput xsi:type='ns:Element' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <rcpGrpRel-collection><rcpGrpRel group-id="1872" recipient-id="1362"></rcpGrpRel></rcpGrpRel-collection>
        </pdomOutput>
      </ExecuteQueryResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

クエリの結果は `<pdomoutput>` 要素から入力されます。

## エラー管理 {#error-management}

SOAP エラー応答の例：

```
<?xml version='1.0' encoding='ISO-8859-1'?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
  <SOAP-ENV:Body>
    <SOAP-ENV:Fault>
      <faultcode>SOAP-ENV:Server</faultcode>
      <faultstring>Error while executing 'Write' of the 'xtk:persist'.</faultstring> service
      <detail>ODBC error: [Microsoft][ODBC SQL Server Driver][SQL Server]Cannot insert duplicate key row in object 'XtkOption' with unique index 'XtkOption_name'. SQLSTate: 23000
ODBC error: [Microsoft][ODBC SQL Server Driver][SQL Server]The statement has been terminated. SQLSTate: 01000 Cannot save the 'Options (xtk:option)' document </detail>
    </SOAP-ENV:Fault>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

SOAP メッセージの本文の `<soap-env:fault>` 要素は、Web サービスの処理中に発生したエラー信号を伝えるために使用されます。 これは、次のサブ要素で構成されます。

* `<faultcode>` :エラーのタイプを示します。エラータイプは次のとおりです。

   * 使用する SOAP バージョンとの非互換性の場合、「VersionMismatch」
   * メッセージヘッダーに問題が発生した場合は、「MustUnderstand」
   * 「クライアント」：クライアントに情報が不足している場合
   * 「サーバー」：サーバーで処理の実行に問題が発生した場合に発生します。

* `<faultstring>` :エラーを説明するメッセージ
* `<detail>` :長いエラーメッセージ

`<faultcode>` 要素を検証すると、サービス呼び出しの成功または失敗が特定されます。

>[!IMPORTANT]
>
>すべてのAdobe Campaign Web サービスはエラーを処理します。 したがって、返されるエラーを処理するために、各呼び出しをテストすることを強くお勧めします。

C#でのエラー処理の例：

```
try 
{
  // Invocation of method
  ...
}
catch (SoapException e)
{
  System.Console.WriteLine("Soap exception: " + e.Message);        
  if (e.Detail != null)
    System.Console.WriteLine(e.Detail.InnerText);
}
```

## Web サービスサーバー（または EndPoint）の URL {#url-of-web-service-server--or-endpoint-}

Web サービスを送信するには、対応するサービスメソッドを実装しているAdobe Campaignサーバーに接続する必要があります。

サーバー URL は次のとおりです。

https://serverName/nl/jsp/soaprouter.jsp

**`<server>`** を使用する場合は、Adobe Campaignアプリケーションサーバー (**nlserver web**)。
