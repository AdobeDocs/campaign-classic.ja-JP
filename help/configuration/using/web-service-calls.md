---
title: Webサービスの呼び出し
seo-title: Webサービスの呼び出し
description: Webサービスの呼び出し
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
source-git-commit: a527f246c4b0bf84c2a83e8df74b7a92542fda7a

---


# Webサービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべてのAPIメソッドは、Webサービスの形式で表示されます。 これにより、Adobe CampaignアプリケーションサーバーのネイティブエントリポイントであるSOAP呼び出しを使用して、すべてのAdobe Campaign機能を管理できます。 Adobe Campaignコンソール自体は、SOAP呼び出しのみを使用します。

Webサービスを使用すると、サードパーティ製システムから多くのアプリケーションを作成できます。

* バックオフィスやトランザクションシステムからの同期アラート、通知、リアルタイム配信テンプレートの実行、
* シンプル化された機能（ウェブインターフェース等）を備えた特殊なインターフェースの開発、
* 基礎となる物理モデルから切り離されたまま、取引ルールを監視しながら、データベース内のデータのフィードと参照を行います。

## Webサービスの定義 {#definition-of-web-services}

Adobe Campaignアプリケーションサーバーに実装されるWebサービスの定義は、データスキーマから使用できます。

Webサービスは、データスキーマの文法で説明され、要素から使用でき **`<methods>`** ます。

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

次に、GenerateFormというメソッドの定義例を示し **ます**。

サービスの説明は要素で始まり `<method>` ます。 メソッドのパラメーターのリストが要素から完了し `<parameters>` ます。 各パラメーターは、名前、タイプ（ブール値、文字列、DOMElementなど）で指定します。と説明。 「inout」属性に「out」値を指定すると、「result」パラメーターがSOAP呼び出し出力にあることを指定できます。

「static」属性（値が「true」の場合）が存在する場合、このメソッドは静的メソッドとして記述され、メソッドのすべてのパラメーターを宣言する必要があります。

「const」メソッドは、関連するスキーマの形式のXMLドキュメントを暗黙的に入力として持ちます。

Adobe Campaignスキーマの要素 `<method>` の詳細については、 <a href="../../configuration/using/elements-and-attributes.md#method--element" target="_blank">  `<method>` エレメント。

「xtk:queryDef」スキーマの「const」型の「ExecuteQuery」メソッドの例：

```
<method name="ExecuteQuery" const="true">
  <help>Retrieve data from a query</help>
  <parameters>
    <param desc="Output xml document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

このメソッドの入力パラメーターは、「xtk:queryDef」スキーマ形式のXMLドキュメントです。

## Webサービスの説明：WSDL {#web-service-description--wsdl}

各サービスでWSDL(Web Service Description Library)ファイルを使用できます。 このXMLファイルは、サービスを記述し、サービスの実行に使用できるメソッド、パラメータ、およびサーバを指定するためにメタ言語を使用します。

### WSDLファイルの生成 {#wsdl-file-generation}

WSDLファイルを生成するには、Webブラウザーから次のURLを入力する必要があります。

[https://`<server>`/nl/jsp/schemawsdl.jsp?schema=`<schema>`

次を含む：

* **`<server>`**:adobe Campaignアプリケーションサーバー(nlserver Web)
* **`<schema>`**:スキーマ識別キー（名前空間：スキーマ名）

### スキーマ&#39;xtk:queryDef&#39;の&#39;ExecuteQuery&#39;メソッドの例 {#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDLファイルはURLから生成されます。

[https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef](https://my_serveur/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef)

WSDLの説明は、まず、Webサービスを形成する「連結」によってプロトコルに接続された、「ポート」に関連付けられたメッセージのフォームに使用する型を定義します。

#### タイプ {#types}

型定義はXMLスキーマに基づいています。 この例では、「ExecuteQuery」メソッドは、「s:string」文字列とXMLドキュメント(`<s:complextype>`)をパラメーターとして受け取ります。 メソッドの戻り値(「ExecuteQueryResponse」)はXMLドキュメント( `<s:complextype>`)です。

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

に、送 `<message>` 信される一連のフィールドの名前とタイプを示します。 このメソッドでは、2つのメッセージを使用して、パラメーター(「ExecuteQueryIn」)と戻り値(「ExecuteQueryOut」)として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

これ `<porttype>` により、応答(「output」)を生成するクエリ(「input」)によってトリガーされる「ExecuteQuery」操作のメッセージが関連付けられます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### 綴じ方 {#binding}

この `<binding>` 部分は、SOAP通信プロトコル( `<soap:binding>` )、HTTPでのデータ転送（「transport」属性の値）、および「ExecuteQuery」操作のデータ形式を指定します。 SOAPエンベロープの本文には、変換を行わずに直接メッセージセグメントが含まれます。

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

ここで `<service>` は、「XtkQueryDef」サービスと、Adobe CampaignアプリケーションサーバーのURL上のURIについて説明します。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続性 {#connectivity}

Adobe Campaignは、セキュリティゾーン(この節の「セキュリティゾーンの定義」を参照 **** )とセッション管理設定を導入することで、認証メカニズムの [セキュリティを強化しました](../../installation/using/configuring-campaign-server.md#defining-security-zones)。

次の2つの認証モードを使用できます。

* **を呼び出します**。 このモードは、セッショントークンとセキュリティトークンを生成します。 これは最も安全なモードであり、最も推奨されるモードです。

または

* **(Adobe Campaignログインと、セッショントークンを作成する** 「パスワード」)を使用します。 セッショントークンは、設定した期間が過ぎると自動的に期限切れになります。 このモードは推奨されません。また、一部のゾーン設定（allowUserPassword=&quot;true&quot;およびsessionTokenOnly=&quot;true&quot;）のアプリケーションセキュリティ設定を減らす必要があります。

### セッショントークンの特性 {#session-token-characteristics}

セッショントークンには、次の特性があります。

* X時間のライフサイクル（ライフサイクルは「serverConf.xml」ファイルで設定でき、デフォルトの期間は24時間です）
* ランダムな構文（ユーザーのログインとパスワードが含まれなくなりました）
* ウェブ経由でアクセスした場合：

   * セッショントークンは永久トークンになり、ブラウザーが閉じても破棄されません
   * これはHTTPのみのcookieに配置されます（演算子の場合はcookieを有効にする必要があります）。

### セキュリティトークンの特性 {#security-token-characteristics}

セキュリティトークンには、次の特性があります。

* セッショントークンから生成されます。
* 24時間のライフサイクル（「serverConf.xml」ファイルで設定可能、デフォルトの期間は24時間）
* Adobe Campaignコンソールに保存されます。
* ウェブ経由でアクセスした場合：

   * ドキュメントに保存されます。__securityTokenプロパティ
   * ページのURLが更新され、セキュリティトークンが更新されます
   * フォームは、トークンを含む非表示のフィールドを介しても更新されます

#### セキュリティトークンの移動 {#security-token-movement}

コンソールからアクセスする場合、次の操作を行います。

* ログオン応答で送信（HTTPヘッダー内）
* （HTTPヘッダー内の）各クエリーで使用

POSTおよびGET HTTPから：

* サーバーは、トークンを使用してリンクを完了します
* サーバーがフォームに非表示フィールドを追加します

SOAP呼び出しから：

* ヘッダーを呼び出すために追加されます。

### 呼び出しの例 {#call-examples}

* HttpSoapConnection/ **SoapServiceの使用**:

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
>次の **HttpServletRequest呼び出しで使用されるURLは** 、 **serverConf.xmlファイルのURL権限セクションにホワイトリストに登録する必要があります** 。 これは、サーバー自体のURLにも当てはまります。

ログオン実行():

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

