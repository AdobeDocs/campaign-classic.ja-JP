---
product: campaign
title: Web サービスの呼び出し
description: Web サービスの呼び出し
feature: API
role: Developer
exl-id: ce94e7e7-b8f8-4c82-937f-e87d15e50c34
TQID: https://experienceleague.adobe.com/-VSnXHtg3Zi3VGHVAF72uRpJa3gulT3h40BIsdnGjqo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 923
ht-degree: 1%

---

# Web サービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべてのAPI メソッドは、Web サービスの形式で表示されます。 これにより、Adobe Campaign アプリケーションサーバーのネイティブエントリポイントであるSOAP呼び出しを介して、すべてのAdobe Campaign関数を管理できます。 Adobe Campaign コンソール自体は、SOAP呼び出しのみを使用します。

Web サービスを使用すると、サードパーティシステムから多くのアプリケーションを作成できます。

* バックオフィスやトランザクションシステムからの同期アラート、通知、リアルタイム配信テンプレートの実行，
* 簡素化された機能（Web インターフェイスなど）を持つ特別なインターフェイスの開発、
* 貿易ルールを観察し、基礎となる物理モデルから分離しながら、データベース内のデータのフィードとルックアップ。

## Web サービスの定義 {#definition-of-web-services}

Adobe Campaign アプリケーションサーバーに実装されたWeb サービスの定義は、データスキーマから使用できます。

Web サービスは、データスキーマの文法で説明され、**`<methods>`**&#x200B;要素から使用できます。

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

ここでは、**GenerateForm**&#x200B;というメソッドの定義の例を示します。

サービスの説明は`<method>`要素で始まります。 メソッドのパラメーターのリストが`<parameters>`要素から完了しました。 各パラメーターは、名前、型（ブール値、文字列、DOMElementなど）で指定します。 簡単に説明できます。 &quot;out&quot;値を持つ&quot;inout&quot;属性を使用すると、&quot;result&quot; パラメーターがSOAP呼び出し出力にあることを指定できます。

「static」属性（値「true」）が存在する場合、このメソッドはstaticとして記述されます。つまり、メソッドのすべてのパラメーターを宣言する必要があります。

「const」メソッドは、関連するスキーマの形式のXML ドキュメントを入力として暗黙的に持ちます。

Adobe Campaign スキーマの`<method>`要素の完全な説明は、[Method](../../configuration/using/schema/method.md)の「スキーマ参照」章で確認できます

「xtk:queryDef」スキーマの「const」型「ExecuteQuery」メソッドの例：

```
<method name="ExecuteQuery" const="true">
  <help>Retrieve data from a query</help>
  <parameters>
    <param desc="Output xml document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

このメソッドの入力パラメーターは、「xtk:queryDef」スキーマ形式のXML ドキュメントです。

## Web サービスの説明：WSDL {#web-service-description--wsdl}

WSDL （Web サービス説明ライブラリ）ファイルは、各サービスに対して使用できます。 このXML ファイルは、メタデータ言語を使用してサービスを記述し、サービスを実行するために使用できるメソッド、パラメーター、および接続するサーバーを指定します。

### WSDL ファイルの生成 {#wsdl-file-generation}

WSDL ファイルを生成するには、Web ブラウザーから次のURLを入力する必要があります。

https://`<server>`/nl/jsp/schemawsdl.jsp?schema=`<schema>`

次の使用条件：

* **`<server>`**: Adobe Campaign アプリケーションサーバー（nlserver web）
* **`<schema>`**: スキーマ識別キー（名前空間:schema_name）

### スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例 {#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDL ファイルは、次のURLから生成されます。

`https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef`

WSDLの説明は、Web サービスを形成する「バインディング」によってプロトコルに接続された「ポート」に関連付けられたメッセージを形成するために使用されるタイプを定義することから始まります。

#### タイプ {#types}

型定義はXML スキーマに基づいています。 この例では、「ExecuteQuery」メソッドは、「s:string」文字列とXML ドキュメント （`<s:complextype>`）をパラメーターとして取ります。 メソッドの戻り値（&quot;ExecuteQueryResponse&quot;）はXML ドキュメント （`<s:complextype>`）です。

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

`<message>`は、送信する一連のフィールドの名前と種類を表します。 メソッドは、2つのメッセージを使用して、パラメーター（「ExecuteQueryIn」）および戻り値（「ExecuteQueryOut」）として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

`<porttype>`は、応答（「output」）を生成するクエリ（「input」）によってトリガーされる「ExecuteQuery」操作に関するメッセージを関連付けます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### 連結 {#binding}

`<binding>`部分は、SOAP通信プロトコル（`<soap:binding>`）、HTTPでのデータトランスポート（「transport」属性の値）、「ExecuteQuery」操作のデータフォーマットを指定します。 SOAP エンベロープの本文には、変換なしでメッセージセグメントが直接含まれています。

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

`<service>`部分は、Adobe Campaign アプリケーションサーバーのURLにURIを含む「XtkQueryDef」サービスについて説明しています。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続性 {#connectivity}

Adobe Campaignでは、[&#x200B; セキュリティゾーン &#x200B;](../../installation/using/security-zones.md)とセッション管理の設定を導入することで、認証メカニズムのセキュリティを強化しました。

使用可能な認証モードは2つあります。

* **ログオン メソッドの呼び出しを介して（）**。 このモードは、セッショントークンおよびセキュリティトークンを生成する。 これは最も安全なモードであり、したがって最も推奨されます。

または

* **セッショントークンを作成するAdobe Campaign ログイン + パスワード**&#x200B;経由。 セッショントークンは、設定された期間が経過すると自動的に期限切れになります。 このモードは推奨されないため、一部のゾーン設定（allowUserPassword=&quot;true&quot;およびsessionTokenOnly=&quot;true&quot;）のアプリケーションセキュリティ設定を減らす必要があります。

### セッショントークンの特徴 {#session-token-characteristics}

セッショントークンには、次の特徴があります。

* x時間のライフサイクル（ライフサイクルは「serverConf.xml」ファイルで設定可能。デフォルトの期間は24時間）
* ランダムな構成（ユーザーのログインとパスワードが含まれなくなりました）
* Web経由でアクセスした場合：

   * セッショントークンは永続的なトークンになり、ブラウザーが閉じても破壊されません
   * http-ONLY Cookieに配置されます（オペレーターにはCookieを有効にする必要があります）

### セキュリティトークンの特徴 {#security-token-characteristics}

セキュリティトークンには、次の特徴があります。

* セッショントークンから生成されます
* ライフサイクルは24時間です（「serverConf.xml」ファイルで設定可能。デフォルトの期間は24時間）
* Adobe Campaign コンソールに保存されます
* Web経由でアクセスした場合：

   * document.securityToken プロパティに格納され__す
   * ページ URLが更新され、セキュリティトークンが更新されます
   * フォームは、トークンを含む非表示のフィールドを介して更新されます

#### セキュリティトークンの移動 {#security-token-movement}

コンソールからアクセスすると、次のようになります。

* （HTTP ヘッダー内の）ログオン応答で送信される
* （HTTP ヘッダー内の）各クエリで使用される

POSTおよびGET HTTPから：

* サーバーは、トークンを使用してリンクを完了します
* サーバーがフォームに非表示フィールドを追加します

SOAP呼び出しから：

* コールヘッダーに追加されます

### 通話例 {#call-examples}

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
>次の&#x200B;**HttpServletRequest**&#x200B;呼び出しで使用されるURLは、**serverConf.xml** ファイルのURL権限セクションで許可リスト上に存在する必要があります。 これは、サーバー自体のURLにも当てはまります。

ログオン実行（）:

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

クエリ実行：

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
