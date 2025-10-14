---
product: campaign
title: Web サービスの呼び出し
description: Web サービスの呼び出し
feature: API
role: Data Engineer, Developer
exl-id: ce94e7e7-b8f8-4c82-937f-e87d15e50c34
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# Web サービスの呼び出し{#web-service-calls}

## 一般情報 {#general-information}

すべての API メソッドは、web サービスの形式で提供されます。 これにより、Adobe Campaign アプリケーションサーバーのネイティブなエントリポイントであるSOAP呼び出しを使用して、すべてのAdobe Campaign関数を管理できます。 Adobe Campaign コンソール自体は、SOAP呼び出しのみを使用します。

Web サービスを使用すると、サードパーティシステムから多くのアプリケーションを作成できます。

* バックオフィスまたはトランザクションシステムからの同期アラート、通知、リアルタイム配信テンプレートの実行
* 機能を簡素化した特別なインターフェイスの開発（Web インターフェイスなど）
* データベース内のデータのフィードと参照を行いながら、トレードルールを観察し、基礎となる物理モデルから分離したままにする。

## Web サービスの定義 {#definition-of-web-services}

Adobe Campaign アプリケーションサーバー上に実装された web サービスの定義は、データスキーマから利用できます。

Web サービスは、データスキーマの文法で記述され、**`<methods>`** 要素から使用できます。

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

**GenerateForm** というメソッドの定義例を次に示します。

サービスの説明は、`<method>` 要素で始まります。 メソッドのパラメーターのリストは、`<parameters>` 要素から完成させます。 各パラメーターは、名前、タイプ（ブール値、文字列、DOMElement など）、説明によって指定されます。 「inout」属性に「out」値を指定すると、「result」パラメーターがSOAP呼び出しの出力にあることを指定できます。

「static」属性（値「true」）が存在する場合、このメソッドは静的であると説明されます。つまり、メソッドのすべてのパラメーターを宣言する必要があります。

「const」メソッドは、関連するスキーマの形式の XML ドキュメントを入力として暗黙的に持ちます。

Adobe Campaign スキーマの `<method>` 要素に関する詳細な説明については、「メソッド [&#x200B; の「スキーマ参照」の章を参照してください &#x200B;](../../configuration/using/schema/method.md)

「xtk:queryDef」スキーマからの「const」タイプの「ExecuteQuery」メソッドの例：

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

WSDL （Web Service Description Library）ファイルは、各サービスで使用できます。 この XML ファイルは、サービスを記述し、サービスの実行に使用できるメソッド、パラメータ、および接続するサーバーを指定するためにメタ言語を使用します。

### WSDL ファイルの生成 {#wsdl-file-generation}

WSDL ファイルを生成するには、web ブラウザーから次の URL を入力する必要があります。

https://`<server>`/nl/jsp/schemawsdl.jsp?schema=`<schema>`

を使用：

* **`<server>`**:Adobe Campaign アプリケーションサーバー（nlserver web）
* **`<schema>`**: スキーマ識別キー（名前空間：schema_name）

### スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例 {#example-on-the--executequery--method-of-schema--xtk-querydef-}

WSDL ファイルは、次の URL から生成されます。

`https://localhost/nl/jsp/schemawsdl.jsp?schema=xtk:queryDef`

WSDL の記述は、まず、Web サービスを形成する「バインディング」によってプロトコルに接続された「ポート」に関連付けられた、メッセージを形成するために使用されるタイプを定義します。

#### タイプ {#types}

タイプの定義は、XML スキーマに基づいています。 この例では、「ExecuteQuery」メソッドは「s:string」文字列と XML ドキュメント（`<s:complextype>`）をパラメーターとして受け取ります。 メソッド（&quot;ExecuteQueryResponse&quot;）の戻り値は XML ドキュメント（`<s:complextype>`）です。

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

`<message>` では、送信する一連のフィールドの名前とタイプについて説明します。 このメソッドは、2 つのメッセージを使用して、をパラメーター（「ExecuteQueryIn」）として渡し、を戻り値（「ExecuteQueryOut」）として渡します。

```
<message name="ExecuteQueryIn">
  <part element="tns:ExecuteQuery" name="parameters"/>
</message>

<message name="ExecuteQueryOut">
  <part element="tns:ExecuteQueryResponse" name="parameters"/>
</message> 
```

#### PortType {#porttype}

`<porttype>` は、応答（「output」）を生成するクエリ（「input」）によってトリガーされる「ExecuteQuery」操作のメッセージを関連付けます。

```
<portType name="queryDefMethodsSoap">
  <operation name="ExecuteQuery">
    <input message="tns:ExecuteQueryIn"/>
    <output message="tns:ExecuteQueryOut"/>
  </operation>
</portType>
```

#### バインディング {#binding}

`<binding>` 部では、SOAP通信プロトコル（`<soap:binding>`）、HTTP でのデータトランスポート（「transport」属性の値）、「ExecuteQuery」オペレーションのデータフォーマットを指定します。 SOAP エンベロープの本文には、変換を行わずにメッセージセグメントが直接含まれます。

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

`<service>` 部では、「XtkQueryDef」サービスと、Adobe Campaign アプリケーションサーバーの URL 上の URI について説明します。

```
<service name="XtkQueryDef">
  <port binding="tns:queryDefMethodsSoap" name="queryDefMethodsSoap">
    <soap:address location="https://localhost/nl/jsp/soaprouter.jsp"/>
  </port>
</service>
```

## 接続性 {#connectivity}

Adobe Campaignでは、[&#x200B; セキュリティゾーン &#x200B;](../../installation/using/security-zones.md) と session management 設定を導入して、認証メカニズムのセキュリティを強化しました。

次の 2 つの認証モードを使用できます。

* **logon メソッド（）の呼び出しを使用**。 このモードは、セッショントークンとセキュリティトークンを生成します。 これは最も安全なモードであるため、最も推奨されます。

または

* セッショントークンを作成する **Adobe Campaign ログイン + パスワードを使用**。 セッショントークンは、設定された期間の後に自動的に期限切れとなります。 このモードはお勧めできません。一部のゾーン設定（allowUserPassword=&quot;true&quot;および sessionTokenOnly=&quot;true&quot;）で、アプリケーションのセキュリティ設定を減らす必要があります。

### セッショントークンの特性 {#session-token-characteristics}

セッショントークンには以下の特徴があります。

* x 時間のライフサイクル（「serverConf.xml」ファイルでライフサイクルを設定できます。デフォルトの期間は 24 時間）
* ランダムな構造（ユーザーのログインとパスワードは含まれなくなりました）
* web 経由でアクセスした場合：

   * セッショントークンは永続的なトークンになり、ブラウザーが閉じると破棄されません
   * これは HTTP 専用の cookie に配置されます（オペレーターは cookie を有効にする必要があります）

### セキュリティトークンの特性 {#security-token-characteristics}

セキュリティトークンには次のような特徴があります。

* セッショントークンから生成されます
* ライフサイクルは 24 時間です（「serverConf.xml」ファイルで設定可能、デフォルトの期間は 24 時間です）
* これは、Adobe Campaign コンソールに保存されます
* web 経由でアクセスした場合：

   * ドキュメントに保存されます。__securityToken プロパティ
   * ページ URL が更新され、セキュリティトークンが更新されます
   * フォームも、トークンを含む非表示フィールドを使用して更新されます

#### セキュリティトークンの移動 {#security-token-movement}

コンソールを介してアクセスした場合、次のようになります。

* ログオン応答で送信（HTTP ヘッダー）
* 各クエリで使用（HTTP ヘッダー内）

POSTおよびGET HTTP から：

* サーバーがトークンでリンクを完了します
* サーバーがフォームに非表示フィールドを追加します

SOAP呼び出しから：

* ヘッダーを呼び出すために追加されます

### 呼び出しの例 {#call-examples}

* **HttpSoapConnection/SoapService** を使用：

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

* **HttpServletRequest** を使用：

>[!NOTE]
>
>次の **HttpServletRequest** 呼び出しで使用される URL は、**serverConf.xml** ファイルの URL permissions セクションで許可リストされている必要があります。 これは、サーバー自体の URL にも当てはまります。

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
