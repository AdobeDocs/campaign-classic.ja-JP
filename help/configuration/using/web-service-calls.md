---
product: campaign
title: Web サービスの呼び出し
description: Web サービスの呼び出し
audience: configuration
content-type: reference
topic-tags: api
exl-id: ce94e7e7-b8f8-4c82-937f-e87d15e50c34
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# Web サービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべてのAPIメソッドは、Webサービスの形式で提供されます。 これにより、Adobe CampaignアプリケーションサーバーのネイティブなエントリポイントであるSOAP呼び出しを介して、すべてのAdobe Campaign関数を管理できます。 Adobe Campaignコンソール自体はSOAP呼び出しのみを使用します。

Webサービスを使用すると、サードパーティシステムから多数のアプリケーションを作成できます。

* バックオフィスやトランザクションシステムからの同期アラート、通知、リアルタイム配信テンプレートの実行
* シンプルな機能（Webインターフェイスなど）を備えた特別なインターフェイスの開発
* 取引ルールを監視し、基礎となる物理モデルから切り離されたまま、データベース内のデータのフィードと検索。

## Webサービスの定義{#definition-of-web-services}

Adobe Campaignアプリケーションサーバーに実装されているWebサービスの定義は、データスキーマから使用できます。

Webサービスは、データスキーマの文法に従って記述され、 **`<methods>`**&#x200B;要素から使用できます。

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

ここでは、**GenerateForm**&#x200B;というメソッドの定義例を示します。

サービスの説明は`<method>`要素で始まります。 メソッドのパラメーターのリストは、`<parameters>`要素から完成します。 各パラメーターは、名前、型（ブール値、文字列、DOMElementなど）で指定します。 説明。 「inout」属性に値「out」を指定すると、「result」パラメーターがSOAP呼び出し出力に含まれるように指定できます。

「static」属性（値が「true」）が存在する場合は、このメソッドが静的メソッドとして記述されます。つまり、メソッドのすべてのパラメーターを宣言する必要があります。

「const」メソッドは、関連するスキーマの形式のXMLドキュメントを暗黙的に入力として持ちます。

Adobe Campaignスキーマの`<method>`要素の詳細な説明は、[メソッド](../../configuration/using/schema/method.md)の下の「スキーマ参照」の章に記載されています

「xtk:queryDef」スキーマの「const」タイプの「ExecuteQuery」メソッドの例：

```
<method name="ExecuteQuery" const="true">
  <help>Retrieve data from a query</help>
  <parameters>
    <param desc="Output xml document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

このメソッドの入力パラメーターは、「xtk:queryDef」スキーマの形式のXMLドキュメントです。

## Webサービスの説明：WSDL {#web-service-description--wsdl}

各サービスにWSDL(Web Service Description Library)ファイルを使用できます。 このXMLファイルは、サービスを記述するメタ言語を使用し、サービスを実行するために接続するメソッド、パラメータ、サーバを指定します。

### WSDLファイル生成{#wsdl-file-generation}

WSDLファイルを生成するには、Webブラウザーから次のURLを入力する必要があります。

https://`<server>`/nl/jsp/schemawsdl.jsp?schema=`<schema>`

次を使用：

* **`<server>`**:Adobe Campaignアプリケーションサーバー(nlserver web)
* **`<schema>`**:スキーマ識別キー(namespace:schema_name)

### スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例{#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDLファイルは次のURLから生成されます。

[https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef](https://my_serveur/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef)

WSDLの説明は、Webサービスを形成する「バインディング」によってプロトコルに接続された「ポート」に関連付けられたメッセージを形成するために使用される型を定義することから始まります。

#### タイプ {#types}

タイプの定義はXMLスキーマに基づいています。 この例では、「ExecuteQuery」メソッドは、「s:string」文字列とXMLドキュメント(`<s:complextype>`)をパラメーターとして取ります。 メソッド(「ExecuteQueryResponse」)の戻り値はXMLドキュメント(`<s:complextype>`)です。

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

`<message>`は、送信する一連のフィールドの名前とタイプを示します。 このメソッドでは、2つのメッセージをパラメーター(「ExecuteQueryIn」)と戻り値(「ExecuteQueryOut」)として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

`<porttype>`は、応答(「output」)を生成するクエリ(「input」)によってトリガーされる「ExecuteQuery」操作に対してメッセージを関連付けます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### バインディング {#binding}

`<binding>`部分は、SOAP通信プロトコル( `<soap:binding>` )、HTTPでのデータ転送（「transport」属性の値）、「ExecuteQuery」操作のデータ形式を指定します。 SOAPエンベロープの本文には、変換を行わずに直接メッセージセグメントが含まれます。

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

`<service>`部分は、「XtkQueryDef」サービスと、Adobe CampaignアプリケーションサーバーのURL上のURIを示します。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続 {#connectivity}

Adobe Campaignは、[セキュリティゾーン](../../installation/using/security-zones.md)とセッション管理の設定を導入することで、認証メカニズムのセキュリティを強化しました。

次の2つの認証モードを使用できます。

* **logon method()の呼び出しを使用する**。このモードでは、セッショントークンとセキュリティトークンが生成されます。 これは最も安全なモードなので、最も推奨されます。

または

* **セッショントークンを作成す** るAdobe Campaignログイン+パスワードを使用する。セッショントークンは、設定された期間が過ぎると自動的に期限切れになります。 このモードは推奨されません。一部のゾーン設定（allowUserPassword=&quot;true&quot;およびsessionTokenOnly=&quot;true&quot;）のアプリケーションセキュリティ設定を減らす必要があります。

### セッショントークンの特性{#session-token-characteristics}

セッショントークンには次の特性があります。

* X時間のライフサイクル（ライフサイクルは「serverConf.xml」ファイルで設定できます。デフォルトの期間は24時間です）
* ランダムな構文（ユーザーのログインとパスワードが含まれなくなりました）
* Web経由でアクセスした場合：

   * セッショントークンは永続トークンになり、ブラウザーが閉じても破棄されません
   * HTTPのみのCookieに配置されます（オペレーターに対してCookieを有効にする必要があります）。

### セキュリティトークンの特性{#security-token-characteristics}

セキュリティトークンには次の特性があります。

* セッショントークンから生成されます。
* 24時間のライフサイクルがあります（「serverConf.xml」ファイルで設定できます。デフォルトの期間は24時間です）。
* これはAdobe Campaignコンソールに保存されます
* Web経由でアクセスした場合：

   * ドキュメントに保存されます。__securityTokenプロパティ
   * ページURLが更新され、セキュリティトークンが更新される
   * フォームは、トークンを含む非表示のフィールドを使用しても更新されます

#### セキュリティトークンの移動{#security-token-movement}

コンソールからアクセスすると、次のようになります。

* ログオン応答（HTTPヘッダー内）で送信されます。
* 各クエリ（HTTPヘッダー内）で使用されます。

POSTとGETHTTPから：

* サーバーがトークンでリンクを完了する
* サーバーがフォームに非表示フィールドを追加する

SOAP呼び出しから：

* 呼び出しヘッダーに追加されます。

### 呼び出し例{#call-examples}

* **HttpSoapConnection/SoapService**&#x200B;を使用：

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

* **HttpServletRequest**&#x200B;を使用：

>[!NOTE]
>
>次の&#x200B;**HttpServletRequest**&#x200B;呼び出しで使用されるURLは、**serverConf.xml**&#x200B;ファイルのurl権限セクションの許可リスト上に存在する必要があります。 これは、サーバー自体のURLに対しても当てはまります。

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
