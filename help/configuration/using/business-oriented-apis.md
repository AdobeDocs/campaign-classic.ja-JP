---
title: ビジネス指向API
seo-title: ビジネス指向API
description: ビジネス指向API
seo-description: null
page-status-flag: never-activated
uuid: ddb6e5cf-dfe0-4dc9-ac5b-fab21827b874
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: e7b3ffca-c85f-498d-89b4-23fcff59de49
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# ビジネス指向API{#business-oriented-apis}

ビジネスAPIは、オブジェクトのタイプごとに異なります。 これらは、次のような効果を持ちます。

* 配信:

   * 配信アクションの作成につい [ては、SubmitDelivery (nms:delivery)](#submitdelivery--nms-delivery-)、
   * キャンペーンの送信（開始、一時停止、停止、証明の送信）、
   * 配信ログの回復

* ワークフロー:

   * ワークフローの開始、
   * プロセスの検証等

      JavaScriptでの [SOAPメソッドを参照してください](../../configuration/using/soap-methods-in-javascript.md)。

* コンテンツ管理
* 購読の管理を参照してくだ [さい。購読(nms:subscription)](#subscribe--nms-subscription-) および [登録解除(nms:subscription)を参照してください](#unsubscribe--nms-subscription-)。
* データプロセス：インポート、エクスポート。

この節では、「購読」、「購読解除」および「配信」サービスの使用について詳しく説明します。

>[!CAUTION]
>
>[キャンペーンJSAPIドキュメントには](http://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html) 、SOAP呼び出しとAdobe CampaignでのJavascriptの使用に関する追加情報に加え、アプリケーションで使用されるすべてのメソッドと関数への完全な参照が含まれています。

## 購読(nms:subscription) {#subscribe--nms-subscription-}

このサービスを使用すると、受信者を情報サービスに登録し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 購読サービスの内部名、
* 受信者情報を含むXMLドキュメント（「nms:recipient」スキーマ）、
* 受信者の作成用のブール値です（まだ存在しない場合）。

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

調整キーの定義は、XMLドキュメントの要素の_**key** 属性を介して入力 `<recipient>` する必要があります。 この属性のコンテンツは、コンマ区切りのXPathリストです。

この呼び出しは、エラー以外のデータを返しません。

### 例 {#examples}

電子メールアドレスの受信者調整キーを持つ購読：入力XMLドキュメントは、電子メールアドレスと、このフィールドのキーの定義を参照する必要があります。

```
<recipient _key="email" email= "john.doe@adobe.com"/>
```

受信者と購読を更新します。

```
<recipient _key="email, [folder-id]" email= "john.doe@adobe.com" folder-id="1305" firstName="John" lastName="Doe"/>
```

### SOAPメッセージの例 {#example-of-soap-messages}

* クエリ:

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

## 登録解除（nms：購読） {#unsubscribe--nms-subscription-}

このサービスを使用すると、受信者を情報サービスから登録解除し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 登録解除するサービスの内部名、
* 受信者情報を含むXMLドキュメント（「nms:recipient」スキーマ）、

「nms:subscription」スキーマの「Unsubscribe」メソッドの説明：

```
<method name="Unsubscribe" static="true">
  <parameters>
    <param name="serviceName" type="string" desc="List of information service names (comma separated)"/>
    <param name="recipient" type="DOMElement"  desc="Recipient"/>
  </parameters>
</method>
```

調整キーの定義は、XMLドキュメントの要素の_key属性を介して入力す `<recipient>` る必要があります。 この属性のコンテンツは、コンマ区切りのXPathリストです。

受信者がデータベースに存在しない場合や、該当する情報サービスに登録されていない場合、サービスは何も実行せず、エラーは生成されません。

>[!NOTE]
>
>サービス名がパラメーターとして指定されていない場合、受信者は自動的にブラックリストに記載されます(@blackList=&quot;1&quot;)。

この呼び出しは、エラー以外のデータを返しません。

### SOAPメッセージの例 {#example-of-soap-messages-1}

クエリ:

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

## SubmitDelivery(nms:delivery) {#submitdelivery--nms-delivery-}

このサービスでは、配信アクションを作成して送信できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 配信テンプレートの内部名、
* 追加の配信データを含むオプションのXMLドキュメント。

このAPIは、パフォーマンスの問題が発生する可能性があるので、ボリューム内で呼び出してはなりません。

スキーマ内のメソッドの説明：

```
<method name="SubmitDelivery" static="true">
  <parameters>
    <param name="scenarioName" type="string" inout="in" desc="Internal name of the delivery template"/>
    <param name="content" type="DOMElement"  inout="in" desc="XML content of the delivery template" />
  </parameters>
</method>
```

配信テンプレートは、Adobe Campaignクライアントコンソールから作成する必要があります。 すべての配信に共通のパラメーター（送信者のアドレスまたはメッセージの有効期間）が含まれます。

入力XMLドキュメントは、「nms:delivery」スキーマの構造に従う配信テンプレートフラグメントです。 配信テンプレートで静的に定義できなかった追加データ（例えば、ターゲットとする受信者のリスト）がすべて含まれます。

この呼び出しは、エラー以外のデータを返しません。

### XMLドキュメントの例 {#xml-document-example}

この例は、外部データソース（この場合はファイル）のカスタム配信テンプレートに基づいています。 設定は配信テンプレートで完全に説明されているので、呼び出しが発生しても送信されないのは要素からのファイルの内容だけ `<externalsource>` です。

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

