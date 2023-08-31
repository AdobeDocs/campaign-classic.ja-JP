---
product: campaign
title: Web サービスの呼び出し
description: Web サービスの呼び出し
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: API
role: Data Engineer, Developer
exl-id: ce94e7e7-b8f8-4c82-937f-e87d15e50c34
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 2%

---

# Web サービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべての API メソッドは、Web サービスの形式で表示されます。 これにより、Adobe Campaignアプリケーションサーバーのネイティブなエントリポイントである SOAP 呼び出しを介して、すべてのAdobe Campaign関数を管理できます。 Adobe Campaignコンソール自体は SOAP 呼び出しのみを使用します。

Web サービスを使用すると、サードパーティのシステムから多数のアプリケーションを作成できます。

* バックオフィスやトランザクションシステムからの同期アラート、通知、リアルタイム配信テンプレートの実行
* シンプルな機能（Web インターフェイスなど）を備えた特別なインターフェイスの開発
* 基になる物理モデルから切り離されたままの取引ルールを監視しながら、データベース内のデータのフィードとルックアップをおこないます。

## Web サービスの定義 {#definition-of-web-services}

Adobe Campaignアプリケーションサーバーに実装されている Web サービスの定義は、データスキーマから使用できます。

Web サービスは、データスキーマの文法に従って記述され、 **`<methods>`** 要素を選択します。

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

以下に、というメソッドの定義例を示します。 **GenerateForm**.

サービスの説明は、 `<method>` 要素を選択します。 メソッドのパラメーターのリストは、  `<parameters>` 要素を選択します。 各パラメーターは、名前、型（ブール値、文字列、DOMElement など）で指定します。 と説明。 「inout」属性を「out」値と共に使用すると、「result」パラメーターが SOAP 呼び出し出力にあることを指定できます。

「static」属性（値が「true」の場合）は、このメソッドを静的メソッドとして記述します。つまり、メソッドのすべてのパラメーターを宣言する必要があります。

&quot;const&quot;メソッドは、関連するスキーマの形式の XML ドキュメントを暗黙的に入力として持っています。

詳しい説明 `<method>` Adobe Campaignスキーマの要素は、下の「スキーマ参照」章にあります。 [メソッド](../../configuration/using/schema/method.md)

「xtk:queryDef」スキーマの「const」タイプ「ExecuteQuery」メソッドの例：

```
<method name="ExecuteQuery" const="true">
  <help>Retrieve data from a query</help>
  <parameters>
    <param desc="Output xml document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

このメソッドの入力パラメーターは、「xtk:queryDef」スキーマの形式の XML ドキュメントです。

## Web サービスの説明：WSDL {#web-service-description--wsdl}

各サービスで WSDL(Web Service Description Library) ファイルを使用できます。 この XML ファイルは、メタ言語を使用してサービスを記述し、サービスを実行するために接続するメソッド、パラメータ、およびサーバを指定します。

### WSDL ファイル生成 {#wsdl-file-generation}

WSDL ファイルを生成するには、Web ブラウザから次の URL を入力する必要があります。

https://`<server>`/nl/jsp/schemawsdl.jsp?schema=`<schema>`

次を使用：

* **`<server>`**:Adobe Campaignアプリケーションサーバー (nlserver web)
* **`<schema>`**：スキーマ識別キー（名前空間：schema_name）

### スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例 {#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDL ファイルは次の URL から生成されます。

`https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef`

WSDL の記述は、Web サービスを形成する「bindings」によってプロトコルに接続された「ports」に関連付けられたメッセージを形成するための型を定義することから始まります。

#### タイプ {#types}

タイプ定義は XML スキーマに基づいています。 この例では、「ExecuteQuery」メソッドは、「s:string」文字列と XML ドキュメント (`<s:complextype>`) をパラメーターとして使用します。 メソッドの戻り値 (「ExecuteQueryResponse」) は XML ドキュメント (  `<s:complextype>`) をクリックします。

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

The `<message>` 送信する一連のフィールドの名前とタイプを示します。 このメソッドでは、2 つのメッセージを使用して、パラメーター (「ExecuteQueryIn」) と戻り値 (「ExecuteQueryOut」) として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

The `<porttype>` 応答 (「output」) を生成するクエリ (「input」) によってトリガーされる「ExecuteQuery」操作に対してメッセージを関連付けます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### 連結 {#binding}

The `<binding>` part は、SOAP 通信プロトコルを指定します ( `<soap:binding>` )、HTTP でのデータ転送（「transport」属性の値）および「ExecuteQuery」操作のデータ形式。 SOAP エンベロープの本文には、変換をおこなわずに、直接メッセージセグメントが含まれます。

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

The `<service>` ここでは、「XtkQueryDef」サービスと、Adobe Campaignアプリケーションサーバーの URL に URI が記述されています。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続 {#connectivity}

Adobe Campaignは、 [セキュリティゾーン](../../installation/using/security-zones.md) およびセッション管理設定。

次の 2 つの認証モードを使用できます。

* **logon method() の呼び出し**. このモードでは、セッショントークンとセキュリティトークンが生成されます。 これは最も安全なモードなので、最も推奨されます。

または

* **Adobe Campaignログインとパスワード** がセッショントークンを作成します。 セッショントークンは、設定された期間が過ぎると自動的に期限切れになります。 このモードは推奨されません。一部のゾーン設定（allowUserPassword=&quot;true&quot;および sessionTokenOnly=&quot;true&quot;）のアプリケーションセキュリティ設定を減らす必要があります。

### セッショントークンの特性 {#session-token-characteristics}

セッショントークンには次の特性があります。

* X 時間のライフサイクル（ライフサイクルは「serverConf.xml」ファイルで設定できます。デフォルトの期間は 24 時間です）
* ランダムな構文（ユーザーのログインとパスワードは含まれなくなりました）
* Web 経由でアクセスした場合：

   * セッショントークンは永続トークンになり、ブラウザーが閉じても破棄されません。
   * HTTP のみの Cookie に配置されます（オペレーターに対して Cookie を有効にする必要があります）。

### セキュリティトークンの特性 {#security-token-characteristics}

セキュリティトークンには次の特性があります。

* セッショントークンから生成されます。
* 24 時間のライフサイクルがあります（「serverConf.xml」ファイルで設定可能、デフォルトの期間は 24 時間です）。
* Adobe Campaignコンソールに保存されます。
* Web 経由でアクセスした場合：

   * ドキュメントに保存されます。__securityToken プロパティ
   * ページの URL が更新され、セキュリティトークンが更新されます
   * フォームは、トークンを含む非表示のフィールドでも更新されます

#### セキュリティトークンの移動 {#security-token-movement}

コンソールからアクセスすると、次のようになります。

* （HTTP ヘッダー内の）ログオン応答で送信されます。
* 各クエリで使用（HTTP ヘッダー内）

POSTとGETHTTP から：

* サーバーがトークンでリンクを完了する
* サーバーがフォームに非表示フィールドを追加します

SOAP 呼び出しから：

* 呼び出しヘッダーに追加されます。

### 呼び出し例 {#call-examples}

* 使用 **HttpSoapConnection/SoapService**:

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

* 使用 **HttpServletRequest**:

>[!NOTE]
>
>次の場合に使用される URL **HttpServletRequest** 呼び出しは、 **serverConf.xml** ファイル。 これは、サーバー自体の URL にも当てはまります。

ログオン実行 ():

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
