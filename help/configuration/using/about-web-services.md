---
product: campaign
title: Web サービスについて
description: Web サービスについて
feature: API
role: Developer
exl-id: 7aa2aef1-2eb6-48a6-82fa-4451bed66216
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 8%

---

# Web サービスについて{#about-web-services}

## Adobe Campaign API の定義 {#definition-of-adobe-campaign-apis}

Adobe Campaign アプリケーションサーバーは、ますます多様化し、複雑さを増す企業の情報システムとのオープンかつ容易な統合を目的として設計されました。

Adobe Campaign API は、アプリケーション内のJavaScriptと、その外部のSOAPで使用されます。 エンリッチメントできる汎用関数のライブラリを構成します。 詳しくは、[SOAP メソッドの実装 &#x200B;](../../configuration/using/implementing-soap-methods.md) を参照してください。

>[!IMPORTANT]
>
>1 日あたりの承認済みエンジンコールの数は、ライセンス契約によって異なります。 詳しくは、[このページ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-classic---product-description.html)を参照してください。\
>すべての API の一覧とその詳細な説明については、[ この専用ドキュメント ] （https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja）を参照してください。

## 前提条件 {#prerequisites}

Adobe Campaign API を使用するには、次のトピックを熟知している必要があります。

* JavaScript
* SOAP プロトコル
* Adobe Campaign データモデル

## Adobe Campaign API の使用 {#using-adobe-campaign-apis}

Adobe Campaignでは、次の 2 種類の API を使用します。

* データモデルデータをクエリするための汎用データアクセス API。[データ指向 API](../../configuration/using/data-oriented-apis.md) を参照してください。
* 目的の対象ごとにアクションをおこなえる、ビジネスに特化した API。配信、ワークフロー、サブスクリプションなど。[&#x200B; ビジネス指向 API](../../configuration/using/business-oriented-apis.md) を参照してください。

API を開発し、Adobe Campaignとやり取りするには、データモデルに関する知識が必要です。 Adobe Campaignでは、ベースの完全な説明を生成できます。 [&#x200B; モデルの説明 &#x200B;](../../configuration/using/data-oriented-apis.md#description-of-the-model) を参照してください。

## SOAP 呼び出し {#soap-calls}

SOAP プロトコルを使用すると、リッチクライアント、web サービスを使用するサードパーティアプリケーション、またはこれらのメソッドをネイティブに使用する JSP を通じて、API メソッドを呼び出すことができます。

![](assets/s_ncs_configuration_architecture.png)

SOAP メッセージの構造は次のとおりです。

* メッセージの構造を定義するエンベロープ。
* オプションのヘッダー。
* 呼び出しと応答に関する情報を含む本文。
* エラー条件を定義するエラー管理。

## リソースと交換 {#resources-and-exchanges}

次のスキーマは、Adobe Campaign API の使用に関連する様々なリソースを示しています。

![](assets/s_ncs_integration_webservices_schema_pres.png)

## 「ExecuteQuery」メソッドのSOAP メッセージの例 {#example-of-a-soap-message-on-the--executequery--method--}

この例では、SOAP クエリは「ExecuteQuery」メソッドを呼び出しています。このメソッドは、認証（セッショントークン）のパラメーターとして文字列を受け取り、実行するクエリの説明の XML コンテンツを実行します。

詳しくは、[ExecuteQuery （xtk:queryDef） &#x200B;](../../configuration/using/data-oriented-apis.md#executequery--xtk-querydef-) を参照してください。

>[!NOTE]
>
>このサービスの WSDL の説明は、次の例のように記述します。[Web サービスの説明：WSDL](../../configuration/using/web-service-calls.md#web-service-description--wsdl)。

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

`<soap-env:envelope>` 要素は、SOAPエンベロープを表すメッセージの最初の要素です。

`<soap-env:body>` 要素は、エンベロープの最初の子要素です。 メッセージの説明、例えば、クエリのコンテンツや応答が含まれています。

呼び出すメソッドを、SOAP メッセージの本文の `<executequery>` 要素に入力します。

SOAPでは、パラメーターは表示順で認識されます。 最初のパラメーター `<__sessiontoken>` は認証チェーンを取り、2 番目のパラメーターは `<querydef>` 要素からのクエリの XML 記述です。

### SOAPの応答 {#soap-response}

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

クエリの結果は、`<pdomoutput>` 要素から入力されます。

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

SOAP メッセージの本文の `<soap-env:fault>` 要素は、web サービスの処理中に発生するエラー信号を伝えるために使用されます。 これは、次のサブ要素で構成されます。

* `<faultcode>`：エラーのタイプを示します。 次のエラータイプがあります。

   * 使用されているSOAPのバージョンと互換性がない場合は、「VersionMismatch」。
   * メッセージヘッダーに問題が発生した場合は、「MustUnderstand」。
   * 「クライアント」：クライアントに情報が不足している場合、
   * 「サーバー」は、サーバーで処理の実行に問題がある場合に表示されます。

* `<faultstring>`：エラーを説明するメッセージ
* `<detail>`：長いエラーメッセージ

サービス呼び出しの成功または失敗は、`<faultcode>` 要素の検証時に識別されます。

>[!IMPORTANT]
>
>すべてのAdobe Campaign Web サービスでエラーが処理されます。 したがって、返されたエラーを処理するために、各呼び出しをテストすることを強くお勧めします。

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

Web サービスを送信するには、対応するサービスメソッドを実装するAdobe Campaign サーバーに接続する必要があります。

サーバー URL は次のとおりです。

https://serverName/nl/jsp/soaprouter.jsp

**`<server>`** をAdobe Campaign アプリケーションサーバー（**nlserver web**）にインストールします。
