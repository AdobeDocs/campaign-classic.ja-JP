---
title: Web サービスについて
seo-title: Web サービスについて
description: Web サービスについて
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
source-git-commit: bc54cef4c44be4c694e062f56685dbb09d2fcf8e
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 5%

---


# Web サービスについて{#about-web-services}

## Adobe CampaignAPIの定義 {#definition-of-adobe-campaign-apis}

Adobe Campaign・アプリケーション・サーバは、ますます多様化し、複雑な会社情報システムとのオープン性と容易な統合を実現するように設計されています。

Adobe CampaignAPIは、アプリケーション内のJavaScriptと、その外部のSOAPで使用されます。 これらは、強化できる汎用関数のライブラリを構成しています。 詳しくは、「SOAPメソッドの [実装](../../configuration/using/implementing-soap-methods.md)」を参照してください。

>[!IMPORTANT]
>
>1日あたりの認定エンジン呼び出し数は、ライセンス契約によって異なります。 詳しくは、[このページ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-classic---product-description.html)を参照してください。\
>すべてのAPIのリスト（詳細な説明を含む）は、 [この専用ドキュメントで入手できます](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)。

## 前提条件 {#prerequisites}

Adobe CampaignAPIを使用する前に、次のトピックに関する知識が必要です。

* JavaScript
* SOAPプロトコル
* Adobe Campaignデータモデル

## Using Adobe Campaign APIs {#using-adobe-campaign-apis}

Adobe Campaignでは、次の2種類のAPIを使用します。

* 汎用データは、データモデルデータをクエリするためのAPIにアクセスします。 詳しくは、 [データ指向APIを参照してください](../../configuration/using/data-oriented-apis.md)。
* 各オブジェクトに対して操作を行えるビジネス固有のAPI:配信、ワークフロー、購読など 「 [ビジネス指向API](../../configuration/using/business-oriented-apis.md)」を参照してください。

APIを開発し、Adobe Campaignとやり取りするには、データモデルに精通している必要があります。 Adobe Campaignを使用すると、基本の完全な説明を生成できます。 「モデルの [説明](../../configuration/using/data-oriented-apis.md#description-of-the-model)」を参照してください。

## SOAP 呼び出し {#soap-calls}

SOAPプロトコルを使用すると、リッチクライアント、Webサービスを使用するサードパーティアプリケーション、またはこれらのメソッドをネイティブで使用するJSP経由でAPIメソッドを呼び出すことができます。

![](assets/s_ncs_configuration_architecture.png)

SOAPメッセージの構造は次のとおりです。

* メッセージの構造を定義する封筒
* オプションのヘッダ、
* 呼び出しと応答に関する情報を含む本文
* エラー条件を定義するエラー管理。

## リソースと交換 {#resources-and-exchanges}

次のスキーマは、Adobe CampaignAPIの使用に関する様々なリソースを示しています。

![](assets/s_ncs_integration_webservices_schema_pres.png)

## &#39;ExecuteQuery&#39;メソッドでのSOAPメッセージの例 {#example-of-a-soap-message-on-the--executequery--method--}

この例では、SOAPクエリが「ExecuteQuery」メソッドを呼び出します。このメソッドは、クエリ（セッショントークン）のパラメーターとして文字列を、実行する認証の説明としてXMLコンテンツを取ります。

詳しくは、ExecuteQuery (xtk:queryDef)を参照し [てください](../../configuration/using/data-oriented-apis.md#executequery--xtk-querydef-)。

>[!NOTE]
>
>このサービスのWSDL説明は、次の例のように入力されています。 [Webサービスの説明：WSDL](../../configuration/using/web-service-calls.md#web-service-description--wsdl)。

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

要素は、SOAPエンベロープを表すメッセージの最初の要素です。 `<soap-env:envelope>`

要素は、エンベロープの最初の子要素です。 `<soap-env:body>` メッセージの説明(クエリの内容や応答など)が含まれます。

呼び出すメソッドは、SOAPメッセージの本文から `<executequery>` 要素に入力されます。

SOAPでは、パラメーターは外観の順序で認識されます。 最初のパラメーター `<__sessiontoken>`は認証チェーンを受け取り、2番目のパラメーターは `<querydef>` 要素からのクエリのXML記述です。

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

クエリの結果は、要素から入力され `<pdomoutput>` ます。

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

SOAPメッセージの本文内の `<soap-env:fault>` 要素は、Webサービスの処理中に発生するエラー信号を伝えるために使用されます。 これは、次のサブ要素で構成されます。

* `<faultcode>` :は、エラーのタイプを示します。 次に、エラータイプを示します。

   * 使用されるSOAPバージョンとの非互換性のイベントに「VersionMismatch」がある。
   * メッセージヘッダー内の問題のイベントに「MustUnderstand」が含まれている場合、
   * クライアントのイベントに「クライアント」が表示され、
   * 「Server」(サーバーで処理の実行に問題があるイベント)。

* `<faultstring>` :エラーを説明するメッセージ
* `<detail>` :長いエラーメッセージ

サービス呼び出しの成功または失敗は、 `<faultcode>` 要素が検証されるときに識別されます。

>[!IMPORTANT]
>
>すべてのAdobe CampaignWebサービスはエラーを処理します。 したがって、返されたエラーを処理するために各呼び出しをテストすることを強くお勧めします。

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

https://serverName/nl/jsp/soaprouter.jsp

Adobe Campaign **`<server>`** アプリケーションサーバー(**nlserver web**)を使用する場合。
