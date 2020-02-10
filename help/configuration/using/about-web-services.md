---
title: Webサービスについて
seo-title: Webサービスについて
description: Webサービスについて
seo-description: null
page-status-flag: never-activated
uuid: f0b21cb3-aa75-4f54-a9f5-64e880f93e53
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 65919173-3ce0-4d98-936b-f4581df536ae
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 34cd6e6cf5652c9e2163848c2b1ef32f53ee6ca4

---


# Webサービスについて{#about-web-services}

## Adobe Campaign APIの定義 {#definition-of-adobe-campaign-apis}

Adobe Campaignアプリケーションサーバーは、ますます多様化し、複雑化する企業情報システムとのオープン性と容易な統合を実現するように設計されています。

Adobe Campaign APIは、アプリケーション内のJavaScriptと、その外部のSOAPで使用されます。 これらは、強化可能な汎用関数のライブラリを構成しています。 詳しくは、「SOAPメソッドの実装」を [参照してください](../../configuration/using/implementing-soap-methods.md)。

>[!CAUTION]
>
>1日あたりの認定エンジンコール数は、ライセンス契約によって異なります。 詳しくは、[このページ](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-classic---product-description.html)を参照してください。\
>詳細な説明を含むすべてのAPIのリストは、この専用ドキュメントで [入手できます](https://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html)。

## 前提条件 {#prerequisites}

Adobe Campaign APIを使用する前に、次のトピックに詳しくなければなりません。

* JavaScript
* SOAPプロトコル
* Adobe Campaignデータモデル

## Adobe Campaign APIの使用 {#using-adobe-campaign-apis}

Adobe Campaignでは、次の2種類のAPIを使用します。

* 汎用データは、データモデルデータをクエリーするためにAPIにアクセスします。 データ指向 [APIを参照](../../configuration/using/data-oriented-apis.md)。
* 各オブジェクトに対して操作を行えるビジネス固有のAPI:配信、ワークフロー、購読など ビジネス指 [向APIを参照](../../configuration/using/business-oriented-apis.md)。

APIを開発し、Adobe Campaignとやり取りするには、データモデルに精通している必要があります。 Adobe Campaignでは、基本の完全な説明を生成できます。 モデルの [説明を参照](../../configuration/using/data-oriented-apis.md#description-of-the-model)。

## SOAP 呼び出し {#soap-calls}

SOAPプロトコルを使用すると、リッチクライアント、Webサービスを使用するサードパーティアプリケーション、またはこれらのメソッドをネイティブに使用するJSPを介してAPIメソッドを呼び出すことができます。

![](assets/s_ncs_configuration_architecture.png)

SOAPメッセージの構造は次のとおりです。

* メッセージの構造を定義する封筒
* オプションのヘッダ、
* 呼び出しと応答に関する情報を含む本体
* エラー条件を定義するエラー管理。

## リソースと交換 {#resources-and-exchanges}

次のスキーマは、Adobe Campaign APIの使用に関連する様々なリソースを示しています。

![](assets/s_ncs_integration_webservices_schema_pres.png)

## 「ExecuteQuery」メソッドでのSOAPメッセージの例 {#example-of-a-soap-message-on-the--executequery--method--}

この例では、SOAPクエリーが「ExecuteQuery」メソッドを呼び出します。このメソッドは、認証用のパラメーターとして文字列（セッショントークン）を、実行するクエリーの説明としてXMLコンテンツを取ります。

詳しくは、ExecuteQuery (xtk:queryDef) [を参照してください](../../configuration/using/data-oriented-apis.md#executequery--xtk-querydef-)。

>[!NOTE]
>
>このサービスのWSDLの説明は、次の例に示すように記述されています。ウェブサ [ービスの説明：WSDL](../../configuration/using/web-service-calls.md#web-service-description--wsdl).

### SOAPクエリ {#soap-query}

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

要素 `<soap-env:envelope>` は、SOAPエンベロープを表すメッセージの最初の要素です。

要素 `<soap-env:body>` は、エンベロープの最初の子要素です。 メッセージの説明（クエリの内容や応答の内容）が含まれます。

呼び出すメソッドは、SOAPメッセージの本 `<executequery>` 文から要素に入力されます。

SOAPでは、パラメータは外観の順序で認識されます。 最初のパラメー `<__sessiontoken>`ターは認証チェーンを受け取り、2番目のパラメーターは要素からのクエリーのXML記述 `<querydef>` です。

### SOAP応答 {#soap-response}

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

クエリーの結果が要素から入力され `<pdomoutput>` ます。

## エラー管理 {#error-management}

SOAPエラー応答の例：

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

SOAPメ `<soap-env:fault>` ッセージの本文内の要素は、Webサービスの処理中に発生するエラー信号を伝えるために使用されます。 これは、次のサブ要素で構成されます。

* `<faultcode>` :エラーのタイプを示します。 エラータイプは次のとおりです。

   * 使用されるSOAPバージョンとの非互換性の場合は、「VersionMismatch」、
   * メッセージヘッダーに問題が発生した場合、「MustUnderstand」
   * 「クライアント」は、クライアントに情報が不足している場合、
   * 「Server」（サーバーで処理の実行に問題がある場合）。

* `<faultstring>` :エラーを説明するメッセージ
* `<detail>` :長いエラーメッセージ

サービス呼び出しの成功または失敗は、要素が検証されると `<faultcode>` 識別されます。

>[!CAUTION]
>
>すべてのAdobe Campaign webサービスはエラーを処理します。 したがって、返されたエラーを処理するために各呼び出しをテストすることを強くお勧めします。

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

## Webサービスサーバー（またはEndPoint）のURL {#url-of-web-service-server--or-endpoint-}

Webサービスを送信するには、対応するサービスメソッドを実装するAdobe Campaignサーバーに接続する必要があります。

サーバーURLは次のとおりです。

[https://`<server>`/nl/jsp/soaprouter.jsp`](https://XXXX//nl/jsp/soaprouter.jsp)

Adobe Campaignア **`<server>`** プリケーションサーバー(**nlserver Web**)を使用します。
