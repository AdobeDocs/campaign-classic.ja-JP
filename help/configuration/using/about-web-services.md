---
product: campaign
title: Web サービスについて
description: Web サービスについて
audience: configuration
content-type: reference
topic-tags: api
exl-id: 7aa2aef1-2eb6-48a6-82fa-4451bed66216
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 12%

---

# Web サービスについて{#about-web-services}

## Adobe Campaign APIの定義{#definition-of-adobe-campaign-apis}

Adobe Campaignアプリケーションサーバは、ますます多様化し、複雑化する企業の情報システムとのオープン性と容易な統合を実現するように設計されています。

Adobe Campaign APIは、アプリケーション内のJavaScriptと、その外部のSOAPで使用されます。 エンリッチメント可能な汎用関数のライブラリを構成します。 詳しくは、[SOAPメソッドの実装](../../configuration/using/implementing-soap-methods.md)を参照してください。

>[!IMPORTANT]
>
>1日あたりの許可されたエンジン呼び出し数は、ライセンス契約によって異なります。 詳しくは、[こちらのページ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-classic---product-description.html)を参照してください。\
>詳細な説明を含むすべてのAPIのリストは、[この専用ドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)で入手できます。

## 前提条件 {#prerequisites}

Adobe Campaign API を使用するには、次のトピックに関する知識が必要です。

* JavaScript
* SOAP プロトコル
* Adobe Campaign データモデル

## Adobe Campaign APIの使用{#using-adobe-campaign-apis}

Adobe Campaignは、次の2種類のAPIを使用します。

* 汎用的なデータアクセス用の API。データモデルの情報をクエリできます。[データ指向 API](../../configuration/using/data-oriented-apis.md) を参照してください。
* 目的の対象ごとにアクションをおこなえる、ビジネスに特化した API。配信、ワークフロー、サブスクリプションなど。[ビジネス指向API](../../configuration/using/business-oriented-apis.md)を参照してください。

APIを開発し、Adobe Campaignとやり取りするには、データモデルに精通している必要があります。 Adobe Campaignを使用すると、ベースの完全な説明を生成できます。 [モデルの説明](../../configuration/using/data-oriented-apis.md#description-of-the-model)を参照してください。

## SOAP 呼び出し {#soap-calls}

SOAPプロトコルを使用すると、リッチクライアント、Webサービスを使用するサードパーティアプリケーション、またはこれらのメソッドをネイティブで使用するJSPを介してAPIメソッドを呼び出すことができます。

![](assets/s_ncs_configuration_architecture.png)

SOAPメッセージの構造を次に示します。

* メッセージの構造を定義する封筒
* オプションのヘッダー
* 呼び出しと応答に関する情報を含む本文
* エラー条件を定義するエラー管理。

## リソースと交換{#resources-and-exchanges}

次のスキーマは、Adobe Campaign APIの使用に関連する様々なリソースを示しています。

![](assets/s_ncs_integration_webservices_schema_pres.png)

## 「ExecuteQuery」メソッド{#example-of-a-soap-message-on-the--executequery--method--}でのSOAPメッセージの例

この例では、SOAPクエリが「ExecuteQuery」メソッドを呼び出します。このメソッドは、文字列を認証用のパラメーター（セッショントークン）とし、XMLコンテンツを取得して実行するクエリを記述します。

詳しくは、[ExecuteQuery (xtk:queryDef)](../../configuration/using/data-oriented-apis.md#executequery--xtk-querydef-)を参照してください。

>[!NOTE]
>
>このサービスのWSDL記述は、次の例に示すように入力されます。[Webサービスの説明：WSDL](../../configuration/using/web-service-calls.md#web-service-description--wsdl)。

### SOAPクエリ{#soap-query}

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

`<soap-env:envelope>`要素は、SOAPエンベロープを表すメッセージの最初の要素です。

`<soap-env:body>`要素は、エンベロープの最初の子要素です。 メッセージの説明（クエリの内容や応答の内容）が含まれます。

呼び出すメソッドは、SOAPメッセージの本文の`<executequery>`要素に入力されます。

SOAPでは、パラメーターは外観の順序で認識されます。 最初のパラメーター`<__sessiontoken>`は認証チェーンを取り、2番目のパラメーターは`<querydef>`要素からのクエリのXML記述です。

### SOAP応答{#soap-response}

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

クエリの結果は`<pdomoutput>`要素から入力されます。

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

SOAPメッセージの本文の`<soap-env:fault>`要素は、Webサービスの処理中に発生するエラー信号を伝達するために使用されます。 これは、次のサブ要素で構成されます。

* `<faultcode>` :エラーのタイプを示します。エラータイプは次のとおりです。

   * 使用するSOAPバージョンとの非互換性の場合、「VersionMismatch」
   * メッセージヘッダーに問題が発生した場合、「MustUnderstand」
   * クライアントに情報が不足している場合の「クライアント」
   * サーバーで処理の実行に問題が発生した場合の「サーバー」。

* `<faultstring>` :エラーを説明するメッセージ
* `<detail>` :長いエラーメッセージ

`<faultcode>`要素を検証すると、サービス呼び出しの成功または失敗が識別されます。

>[!IMPORTANT]
>
>すべてのAdobe Campaign Webサービスでエラーが処理されます。 したがって、返されるエラーを処理するために、各呼び出しをテストすることを強くお勧めします。

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

Adobe Campaignアプリケーションサーバー(**`<server>`** nlserver web **)を**&#x200B;使用します。
