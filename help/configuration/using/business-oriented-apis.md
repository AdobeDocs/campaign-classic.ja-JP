---
product: campaign
title: ビジネス指向の API
description: ビジネス指向の API
feature: API
role: Data Engineer, Developer
exl-id: e6638870-3141-4f12-b904-db436127c0d1
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# ビジネス指向の API{#business-oriented-apis}

ビジネス API は、オブジェクトのタイプごとに固有です。 次の項目に影響します。

* 配信 :

   * 配信アクションの作成。[SubmitDelivery （nms:delivery） ](#submitdelivery--nms-delivery-) を参照してください。
   * キャンペーンの送信（開始、一時停止、停止、配達確認の送信）、
   * 配信ログを復元しています。

* ワークフロー：

   * ワークフローの開始
   * 工程の検証等

     JavaScriptの [SOAP メソッドを参照してください ](../../configuration/using/soap-methods-in-javascript.md)。

* コンテンツ管理
* 購読の管理。[ 購読（nms:subscription） ](#subscribe--nms-subscription-) および [ 購読解除（nms:subscription） ](#unsubscribe--nms-subscription-) を参照してください。
* データプロセス：インポート、エクスポート。

この節では、「購読」、「購読解除」、「SubmitDelivery」の各サービスの使用方法について説明します。

>[!IMPORTANT]
>
>[Campaign JSAPI ドキュメント ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja) には、SOAP呼び出しとAdobe Campaignでの JavaScript 使用に関する追加情報のほか、アプリケーションで使用されるすべてのメソッドと関数の完全なリファレンスが含まれています。

## 購読（nms:subscription） {#subscribe--nms-subscription-}

このサービスを使用すると、受信者を情報サービスに登録して、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証、
* 購読サービスの内部名。
* 受信者情報を含む XML ドキュメント（「nms:recipient」スキーマから）
* 受信者作成用のブール値（まだ存在しない場合）。

「nms:subscription」スキーマの「subscribe」メソッドの説明：

```
<method name="Subscribe" static="true">
  <parameters>
     <param name="serviceName" type="string"  desc="List of information service names (comma separated)"/>
     <param name="recipient" type="DOMElement" desc="Recipient"/>
     <param name="create" type="Boolean" desc="Create recipient if it does not exist"/>
   </parameters>
</method>
```

紐付けキーの定義は、XML ドキュメントの `<recipient>` 要素の_&#x200B;**key** 属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りの XPath リストです。

この呼び出しは、エラーを除き、データを返しません。

### 例 {#examples}

メールアドレスに受信者紐付けキーを使用した購読：入力 XML ドキュメントは、メールアドレスとこのフィールドのキーの定義を参照する必要があります。

```
<recipient _key="email" email= "john.doe@adobe.com"/>
```

受信者とサブスクリプションを更新します。

```
<recipient _key="email, [folder-id]" email= "john.doe@adobe.com" folder-id="1305" firstName="John" lastName="Doe"/>
```

### SOAP メッセージの例 {#example-of-soap-messages}

* クエリ :

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <m:Subscribe xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <sessiontoken xsi:type='xsd:string'/>
        <service xsi:type='xsd:string'>SVC1</service>
        <content xsi:type='' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <recipient _key="@email" email= "john.doe@adobe.com/>
        </content>
        <create xsi:type='xsd:boolean'>true</create>
      </m:Subscribe>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

* 応答：

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <m:SubscribeResponse xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
      </m:SubscribeResponse>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

## 購読解除（nms:subscription） {#unsubscribe--nms-subscription-}

このサービスを使用すると、情報サービスの受信者を登録解除して、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証、
* 購読解除するサービスの内部名。
* 受信者情報を含む XML ドキュメント（「nms:recipient」スキーマから）

「nms:subscription」スキーマの「購読解除」メソッドの説明：

```
<method name="Unsubscribe" static="true">
  <parameters>
    <param name="serviceName" type="string" desc="List of information service names (comma separated)"/>
    <param name="recipient" type="DOMElement"  desc="Recipient"/>
  </parameters>
</method>
```

紐付けキーの定義は、XML ドキュメントの `<recipient>` 要素の_key 属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りの XPath リストです。

受信者がデータベースに存在しない場合や、該当する情報サービスを購読していない場合、サービスはアクションを実行せず、エラーは生成されません。

>[!NOTE]
>
>ブロックリストに加える @blackList サービス名をパラメーターとして指定しない場合、受信者は自動的に on になります。

この呼び出しは、エラーを除き、データを返しません。

### SOAP メッセージの例 {#example-of-soap-messages-1}

クエリ :

```
<?xml version='1.0' encoding='ISO-8859-1'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
  <SOAP-ENV:Body>
    <m:Unsubscribe xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
    <sessiontoken xsi:type='xsd:string'/>
    <service xsi:type='xsd:string'>SVC1</service>
    <content xsi:type='' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
      <recipient _key="@email" email= "john.doe@adobe.com/>
    </content>
  </m:Unsubscribe>
</SOAP-ENV:Body>
```

応答：

```
<?xml version='1.0' encoding='ISO-8859-1'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
  <SOAP-ENV:Body>
    <m:UnsubscribeResponse xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
    </m:UnsubscribeResponse>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## SubmitDelivery （nms:delivery） {#submitdelivery--nms-delivery-}

このサービスを使用すると、配信アクションを作成して送信できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証、
* 配信テンプレートの内部名
* 追加の配信データを含むオプションの XML ドキュメント。

パフォーマンスの問題が発生する可能性があるので、この API を大量に呼び出さないでください。

スキーマ内のメソッドの説明：

```
<method name="SubmitDelivery" static="true">
  <parameters>
    <param name="scenarioName" type="string" inout="in" desc="Internal name of the delivery template"/>
    <param name="content" type="DOMElement"  inout="in" desc="XML content of the delivery template" />
  </parameters>
</method>
```

配信テンプレートは、Adobe Campaign クライアントコンソールから作成する必要があります。 すべての配信に共通のパラメーター（送信者アドレスまたはメッセージの有効期間）が含まれます。

入力 XML ドキュメントは、「nms:delivery」スキーマの構造に従う配信テンプレートフラグメントです。 配信テンプレートに静的に定義できなかった追加データ（ターゲットとする受信者のリストなど）がすべて含まれます。

この呼び出しは、エラーを除き、データを返しません。

### XML ドキュメントの例 {#xml-document-example}

この例は、外部データソース（この場合はファイル）のカスタム配信テンプレートに基づいています。 設定は配信テンプレートで完全に記述されているので、呼び出しが発生した場合に送信されるのは、`<externalsource>` 要素のファイルのコンテンツだけです。

```
<delivery>
  <targets fromExternalSource="true">
    <externalSource>
      MsgId|ClientId|Title|Name|FirstName| Mobile|Email| Market_segment|Product_affinity1 |Product_affinity2|Product_affinity3| Product_affinity4| Support_Number|Amount|Threshold1|000001234|M.| Doe|John|0650201020| john.doe@adobe.com
|1| A1|A2|A3|A4|E12|120000|100000
    </externalSource>
  </target>
</delivery>
```

配信テンプレートがない場合は、次のサンプルを使用できます。

```
<delivery>
<targets fromExternalSource="true" targetMode="1" noReconciliation="true" addressField="Email" >  
    <fileFormat active="true">  
      <source format="text" type="text">  
        <dataSourceConfig >  
          <dataSourceColumn label="Email" name="Email" type="string"/>  
        </dataSourceConfig>  
      </source>  
      <destination type="xtkDataStore"/>  
    </fileFormat>  
    <externalSource><![CDATA[not-a-repicipient@domain.com]]></externalSource>  
  </targets> 
</delivery> 
```
