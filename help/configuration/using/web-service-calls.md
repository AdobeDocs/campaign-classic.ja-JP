---
title: Web サービスの呼び出し
seo-title: Web サービスの呼び出し
description: Web サービスの呼び出し
seo-description: null
page-status-flag: never-activated
uuid: 7defe0e4-bb4a-4f6a-b6e8-e2ffac73b4c1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 6934c165-6d27-4ce5-8607-170f299b4702
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 3b752b283a14bc75954fe46da5a21970c1e17fa1
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---


# Web サービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべてのAPIメソッドは、Webサービスの形式で表示されます。 これにより、SOAP呼び出し(Adobe Campaignアプリケーションサーバーのネイティブエントリポイント)を介して、すべてのAdobe Campaign機能を管理できます。 Adobe Campaignコンソール自体は、SOAP呼び出しのみを使用します。

Webサービスを使用すると、サードパーティ製システムから多くのアプリケーションを作成できます。

* バック・オフィスやトランザクション・システムからの同期アラート、通知、リアルタイム・配信テンプレート実行、
* シンプルな機能（Webインターフェイスなど）を備えた特殊なインターフェースの開発、
* 取引ルールを監視しながら、基礎となる物理モデルから隔離された状態で、データベース内のデータのフィードと参照を行う。

## Webサービスの定義 {#definition-of-web-services}

Adobe Campaignアプリケーションサーバーに実装されるWebサービスの定義は、データスキーマから利用できます。

Webサービスは、データ要素の文法で記述され、 **`<methods>`** 要素から使用できます。

```
<methods>
  <method name="GenerateForm" static="true">
    <help>Generates the form in Mail or Web mode</help>
    <parameters>
      <param name="formName" type="string" desc="Name of form"/>
      <param name="mailMode" type="boolean" desc="Generate a form of type Mail"/>
      <param name="result" type="string" inout="out" desc="Result "/>
    </parameters>
  </method>
</methods>
```

ここでは、GenerateFormというメソッドの定義例を示し **ます**。

要素を含むサービス開始の説明 `<method>` です。 メソッドのパラメータのリストは、 `<parameters>` 要素から完了します。 各パラメーターは、名前、型（ブール値、文字列、DOMElementなど）で指定します。 と説明。 「inout」属性で「out」値を指定すると、「result」パラメーターがSOAP呼び出し出力にあることを指定できます。

「static」属性（値が「true」の場合）は、このメソッドを静的メソッドとして記述します。つまり、メソッドのすべてのパラメーターを宣言する必要があります。

&quot;const&quot;メソッドは暗黙的に、関連するスキーマの形式のXMLドキュメントを入力として持ちます。

Adobe Campaignスキーマの `<method>` 要素の詳細な説明は、「スキーマ参照」の章(  <a href="../../configuration/using/elements-and-attributes.md#method--element" target="_blank">  `<method>`要素にオファーコンテンツが返されます。

「xtk:queryDef」スキーマの&quot;const&quot;型の&quot;ExecuteQuery&quot;メソッドの例：

```
<method name="ExecuteQuery" const="true">
  <help>Retrieve data from a query</help>
  <parameters>
    <param desc="Output xml document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

このメソッドの入力パラメータは、&quot;xtk:queryDef&quot;スキーマの形式のXMLドキュメントです。

## Webサービスの説明：WSDL {#web-service-description--wsdl}

各サービスでWSDL(Web Service Description Library)ファイルを使用できます。 このXMLファイルは、サービスの説明、およびサービスの実行に使用する接続のための利用可能なメソッド、パラメータ、サーバを指定するためにメタ言語を使用します。

### WSDLファイルの生成 {#wsdl-file-generation}

WSDLファイルを生成するには、Webブラウザから次のURLを入力する必要があります。

https://`<server>`/nl/jsp/schemawsdl.jsp?スキーマ=`<schema>`

次を含む：

* **`<server>`**:adobe campaignアプリケーションサーバー(nlserver web)
* **`<schema>`**:スキーマIDキー(名前空間:スキーマ名)

### スキーマ&#39;xtk:queryDef&#39;の&#39;ExecuteQuery&#39;メソッドの例 {#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDLファイルは次のURLから生成されます。

[https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef](https://my_serveur/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef)

WSDL記述開始。Webサービスを形成する「バインディング」によって、プロトコルに接続された「ポート」に関連付けられたメッセージのフォームに使用する型を定義します。

#### タイプ {#types}

型の定義は、XMLスキーマに基づいています。 この例では、「ExecuteQuery」メソッドは、「s:string」文字列とXMLドキュメント(`<s:complextype>`)をパラメーターとして受け取ります。 メソッドの戻り値(「ExecuteQueryResponse」)はXMLドキュメント( `<s:complextype>`)です。

```
<types>
<s:schema elementFormDefault="qualified" targetNamespace="urn:xtk:queryDef">
  <s:element name="ExecuteQuery">
    <s:complexType>
      <s:sequence>
        <s:element maxOccurs="1" minOccurs="1" name="sessiontoken" type="s:string"/>
        <s:element maxOccurs="1" minOccurs="1" name="entity">
          <s:complexType>
            <s:sequence>
              <s:any/>
            </s:sequence>
          </s:complexType>
        </s:element>
      </s:sequence>
    </s:complexType>
  </s:element>
  <s:element name="ExecuteQueryResponse">
    <s:complexType>
      <s:sequence>
        <s:element maxOccurs="1" minOccurs="1" name="pdomOutput">
          <s:complexType mixed="true">
            <s:sequence>
              <s:any/>
            </s:sequence>
          </s:complexType>
        </s:element>
      </s:sequence>
    </s:complexType>
  </s:element>
```

#### メッセージ {#messages}

に、送信する一連のフィールドの名前と種類を `<message>` 示します。 このメソッドでは、2つのメッセージを使用して、パラメーター(「ExecuteQueryIn」)と戻り値(「ExecuteQueryOut」)として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

この `<porttype>` 関数は、「ExecuteQuery」操作でクエリ(「input」)が応答(「output」)を生成することによってトリガーされるメッセージを関連付けます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### 綴じ方 {#binding}

この `<binding>` 部分では、SOAP通信プロトコル( `<soap:binding>` )、HTTPでのデータ転送（ 「transport」属性の値）、および「ExecuteQuery」操作のデータ形式を指定します。 SOAPエンベロープの本文には、変換を行わずに直接メッセージセグメントが含まれます。

```
<binding name="queryDefMethodsSoap" type="tns:queryDefMethodsSoap">
  <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
  <operation name="ExecuteQuery">
    <soap:operation soapAction="xtk:queryDef#ExecuteQuery" style="document"/>
    <input>
      <soap:body encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" namespace="urn:xtk:queryDef" use="literal"/>
    </input>
    <output>
      <soap:body encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" namespace="urn:xtk:queryDef" use="literal"/>
    </output>
  </operation>
</binding>
```

#### サービス {#service}

この `<service>` 部分は、Adobe CampaignアプリケーションサーバーのURLにURIを持つ「XtkQueryDef」サービスについて説明しています。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続性 {#connectivity}

Adobe Campaignは、セキュリティゾーンの導入( **この節の「セキュリティゾーンの** 定義 [」の章を参照](../../installation/using/configuring-campaign-server.md#defining-security-zones))とセッション管理設定により、認証メカニズムのセキュリティを強化しました。

次の2つの認証モードを使用できます。

* **を呼び出して、logon method()**. このモードは、セッショントークンとセキュリティトークンを生成します。 これは最も安全なモードであるため、最も推奨されるモードです。

または

* **adobe campaignログインと、セッショントークンを作成するパスワード** 。 セッショントークンは、設定した期間が過ぎると自動的に期限切れになります。 このモードは推奨されないため、一部のゾーン設定（allowUserPassword=&quot;true&quot;およびsessionTokenOnly=&quot;true&quot;）のアプリケーションセキュリティ設定を減らす必要があります。

### セッショントークンの特性 {#session-token-characteristics}

セッショントークンには、次の特性があります。

* X時間のライフサイクル（ライフサイクルは「serverConf.xml」ファイルで設定でき、デフォルトの期間は24時間です）
* ランダムな構文（ユーザーのログインとパスワードが含まれなくなりました）
* ウェブ経由でアクセスした場合：

   * セッショントークンは永久トークンになり、ブラウザーが閉じても破棄されません
   * このcookieはHTTPのみのcookieに配置されます（演算子の場合はcookieをアクティブにする必要があります）。

### セキュリティトークンの特性 {#security-token-characteristics}

セキュリティトークンには、次の特性があります。

* セッショントークンから生成されます。
* ライフサイクルは24時間です（「serverConf.xml」ファイルで設定できます。デフォルトの期間は24時間です）
* adobe campaignコンソールに保存されます。
* ウェブ経由でアクセスした場合：

   * ドキュメントーに保存されます。__securityTokenプロパティ
   * ページのURLが更新され、セキュリティトークンが更新されます。
   * フォームは、トークンを含む非表示のフィールドを介しても更新されます

#### セキュリティトークンの移動 {#security-token-movement}

コンソールからアクセスする場合、次の操作を行います。

* ログオン応答（HTTPヘッダー内）で送信される
* 各クエリで使用（HTTPヘッダー内）

POSTとGETHTTPから：

* サーバーはトークンを使用してリンクを完了します
* サーバーがフォームに非表示フィールドを追加

SOAP呼び出しからの場合：

* 呼び出しヘッダーに追加されます。

### 呼び出しの例 {#call-examples}

* HttpSoapConnection/SoapService **の使用**:

```
  
    var cnx = new HttpSoapConnection("https://serverURL/nl/jsp/soaprouter.jsp");
  var session = new SoapService(cnx, 'urn:xtk:session');
  session.addMethod("Logon", "xtk:session#Logon",
                      ["sessiontoken", "string", "Login", "string", "Password", "string", "Parameters", "NLElement"],
                      ["sessionToken", "string", "sessionInfo", "NLElement", "securityToken", "string"]);
  
  var res = session.Logon("", "admin", "pwd", <param/>);
  var sessionToken = res[0];
  var securityToken = res[2];
  
  cnx.addTokens(sessionToken, securityToken);
  var query = new SoapService(cnx, 'urn:xtk:queryDef');
  query.addMethod("ExecuteQuery", "xtk:queryDef#ExecuteQuery",
                      ["sessiontoken", "string", "entity", "NLElement"],
                      ["res", "NLElement"]);
  
  var queryRes = query.ExecuteQuery("", <queryDef operation="select" schema="nms:recipient">
            <select>
              <node expr="@email"/>
              <node expr="@lastName"/>
              <node expr="@firstName"/>
            </select>
            <where>
              <condition expr="@email = 'joe.doe@aol.com'"/>
            </where>
          </queryDef>);
  logInfo(queryRes[0].toXMLString())
```

* HttpServletRequest **の使用**:

>[!NOTE]
>
>以下のHttpServletRequest **呼び出しで使用されるURLは、** serverConf.xml **** ファイルのurl権限セクションの許可リスト上に存在する必要があります。 これは、サーバー自体のURLに対しても同じです。

ログオンの実行():

```
var req = new HttpClientRequest("https://serverURL/nl/jsp/soaprouter.jsp");
req.header["Content-Type"] = "text/xml; charset=utf-8";
req.header["SOAPAction"] =   "xtk:session#Logon";
req.method = "POST";
req.body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:session">' +
    '<soapenv:Header/>' +
    '<soapenv:Body>' +
        '<urn:Logon>' +
            '<urn:sessiontoken></urn:sessiontoken>' +
            '<urn:strLogin>LOGIN_HERE</urn:strLogin>' +
            '<urn:strPassword>PASSWORD_HERE</urn:strPassword>' +
            '<urn:elemParameters></urn:elemParameters>' +
        '</urn:Logon>' +
    '</soapenv:Body>' +
'</soapenv:Envelope>';
req.execute();
           
var resp = req.response;
var xmlRes = new XML(String(resp.body).replace("<?xml version='1.0'?>",""));
var sessionToken = String(xmlRes..*::pstrSessionToken);;
var securityToken = String(xmlRes..*::pstrSecurityToken);
```

クエリの実行：

```
var req2 = new HttpClientRequest("https://serverURL/nl/jsp/soaprouter.jsp");
req2.header["Content-Type"] = "text/xml; charset=utf-8";
req2.header["SOAPAction"] =   "xtk:queryDef#ExecuteQuery";req2.header["X-Security-Token"] = securityToken;
req2.header["cookie"]           = "__sessiontoken="+sessionToken;
req2.method = "POST";
req2.body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:queryDef">' +
             '<soapenv:Header/><soapenv:Body><urn:ExecuteQuery><urn:sessiontoken/><urn:entity>' +
                '<queryDef operation="select" schema="nms:recipient">' +
                  '<select><node expr="@email"/><node expr="@lastName"/><node expr="@firstName"/></select>' +
                  '<where><condition expr="@email = \'john.doe@aol.com\'"/></where>' +
                '</queryDef>' +
           '</urn:entity></urn:ExecuteQuery></soapenv:Body></soapenv:Envelope>';
req2.execute();
var resp2 = req2.response;
logInfo(resp2.body)
```
