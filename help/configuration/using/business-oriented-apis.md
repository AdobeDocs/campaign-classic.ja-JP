---
product: campaign
title: ビジネス指向の API
description: ビジネス指向の API
feature: API
role: Developer
exl-id: e6638870-3141-4f12-b904-db436127c0d1
TQID: https://experienceleague.adobe.com/lPAawM33zS2tws0EyHFHW1jD-Vw3ZLDtDcMEd1eJA1c
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b12f6872-9271-4369-85e5-86969a0b99a2
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 3%

---

# ビジネス指向の API{#business-oriented-apis}

Business APIは、オブジェクトの各タイプに固有です。 これには、次のような効果があります。

* 配信 :

   * 配信アクションの作成については、[SubmitDelivery （nms:delivery） ](#submitdelivery--nms-delivery-)を参照してください。
   * キャンペーンの送信（開始、一時停止、停止、プルーフの送信）,
   * 配信ログを復元しています。

* ワークフロー：

   * ワークフローを開始するには，
   * プロセスの検証等

     JavaScript](../../configuration/using/soap-methods-in-javascript.md)の[SOAP メソッドを参照してください。

* コンテンツ管理
* サブスクリプション管理については、[購読（nms:subscription） ](#subscribe--nms-subscription-)および[購読解除（nms:subscription） ](#unsubscribe--nms-subscription-)を参照してください。
* データプロセス：インポート、エクスポート。

この節では、「Subscribe」、「Unsubscribe」および「SubmitDelivery」サービスの使用について詳しく説明します。

>[!IMPORTANT]
>
>[Campaign JSAPI ドキュメント ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja)には、SOAPの呼び出しとAdobe CampaignでのJavascriptの使用に関する詳細情報と、アプリケーションで使用されるすべてのメソッドと関数への完全な参照が含まれています。

## 購入（nms:subscription） {#subscribe--nms-subscription-}

このサービスでは、受信者を情報サービスに登録し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証，
* サブスクリプションサービスの内部名，
* 受信者情報（「nms:recipient」スキーマから）を含むXML ドキュメント
* 受信者がまだ作成していない場合は、受信者作成のブール値。

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

紐付けキーの定義は、XML ドキュメントの`<recipient>`要素の_**key**&#x200B;属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りのXPath リストです。

この呼び出しは、エラー以外のデータを返しません。

### 例 {#examples}

電子メールアドレスに受信者紐付けキーを含むサブスクリプション：入力XML ドキュメントは、電子メールアドレスとこのフィールドのキーの定義を参照する必要があります。

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

## 登録解除（nms:subscription） {#unsubscribe--nms-subscription-}

このサービスを使用すると、情報サービスから受信者の購読を解除し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証，
* 購読を解除するサービスの内部名
* 受信者情報（「nms:recipient」スキーマから）を含むXML ドキュメント

「nms:subscription」スキーマの「購読解除」メソッドの説明：

```
<method name="Unsubscribe" static="true">
  <parameters>
    <param name="serviceName" type="string" desc="List of information service names (comma separated)"/>
    <param name="recipient" type="DOMElement"  desc="Recipient"/>
  </parameters>
</method>
```

紐付けキーの定義は、XML ドキュメントの`<recipient>`要素の_key属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りのXPath リストです。

受信者がデータベースに存在しないか、関連する情報サービスを購読していない場合、サービスはアクションを実行せず、エラーは生成されません。

>[!NOTE]
>
>サービス名がパラメーターとして指定されていない場合、受信者は自動的にブロックリスト（@blackList=&quot;1&quot;）に移動します。

この呼び出しは、エラー以外のデータを返しません。

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

このサービスでは、配信アクションを作成して送信できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証，
* 配信テンプレートの内部名。
* 追加の配信データを含むオプションのXML ドキュメント。

パフォーマンスの問題が発生する可能性があるため、このAPIはボリュームで呼び出さないでください。

スキーマ内のメソッドの説明：

```
<method name="SubmitDelivery" static="true">
  <parameters>
    <param name="scenarioName" type="string" inout="in" desc="Internal name of the delivery template"/>
    <param name="content" type="DOMElement"  inout="in" desc="XML content of the delivery template" />
  </parameters>
</method>
```

配信テンプレートは、Adobe Campaign クライアントコンソールから作成する必要があります。 すべての配信（送信者のアドレスまたはメッセージの有効期間）に共通するパラメーターが含まれます。

入力XML ドキュメントは、「nms:delivery」スキーマの構造に従う配信テンプレートフラグメントです。 配信テンプレートで静的に定義できなかった追加データ（ターゲットとなる受信者のリストなど）がすべて含まれます。

この呼び出しは、エラー以外のデータを返しません。

### XML ドキュメントの例 {#xml-document-example}

この例は、外部データソース（この場合はファイル）からのカスタム配信テンプレートに基づいています。 設定は配信テンプレートに完全に記述されているため、呼び出しが発生したときに送信される残りはすべて、`<externalsource>`要素からのファイルの内容です。

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
