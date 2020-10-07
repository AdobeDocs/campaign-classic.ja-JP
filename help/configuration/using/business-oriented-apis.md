---
title: ビジネス指向 API
seo-title: ビジネス指向 API
description: ビジネス指向 API
seo-description: null
page-status-flag: never-activated
uuid: ddb6e5cf-dfe0-4dc9-ac5b-fab21827b874
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: e7b3ffca-c85f-498d-89b4-23fcff59de49
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# ビジネス指向 API{#business-oriented-apis}

ビジネスAPIは、オブジェクトのタイプごとに異なります。 これらは次のような影響を与えます。

* 配信:

   * 配信アクションの作成については、SubmitDelivery(nms: [配信)](#submitdelivery--nms-delivery-)、
   * キャンペーン(開始、一時停止、停止、送信配達確認)の送信、
   * 配信ログの回復

* ワークフロー:

   * ワークフローの開始、
   * プロセスの検証等

      JavaScriptでの [SOAPメソッドを参照してください](../../configuration/using/soap-methods-in-javascript.md)。

* コンテンツ管理
* 購読管理については、「 [サブスクライブ(nms:購読)](#subscribe--nms-subscription-) 」および「 [登録解除(nms:購読)」を参照してください](#unsubscribe--nms-subscription-)。
* データプロセス：インポート、エクスポート。

この節では、「Subscribe」、「Unsubscribe」および「SubmitDelivery」サービスの使用について詳しく説明します。

>[!IMPORTANT]
>
>[キャンペーンJSAPIドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html) には、SOAP呼び出しとAdobe CampaignでのJavaScriptの使用に関する追加情報に加え、アプリケーションで使用されるすべてのメソッドと関数への完全な参照が含まれています。

## 購読(nms:購読) {#subscribe--nms-subscription-}

このサービスを使用すると、情報サービスへの受信者を登録し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 購読サービスの内部名、
* 受信者ドキュメント(「nms:受信者」スキーマ)を含むXML情報、
* 受信者作成用のブール値（まだない場合）。

「nms:購読」スキーマ内の「subscribe」メソッドの説明：

```
<method name="Subscribe" static="true">
  <parameters>
     <param name="serviceName" type="string"  desc="List of information service names (comma separated)"/>
     <param name="recipient" type="DOMElement" desc="Recipient"/>
     <param name="create" type="Boolean" desc="Create recipient if it does not exist"/>
   </parameters>
</method>
```

紐付けキーの定義は、XMLドキュメントの&#x200B;**要素の_** key `<recipient>` 属性を介して入力する必要があります。 この属性の内容は、コンマ区切りのXPathリストです。

この呼び出しは、エラー以外のデータを返しません。

### 例 {#examples}

電子メールアドレスに受信者紐付けキーがある購読:入力XMLドキュメントは、電子メールアドレスと、このフィールドのキーの定義を参照する必要があります。

```
<recipient _key="email" email= "john.doe@adobe.com"/>
```

購読と受信者の更新。

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

* 応答:

   ```
   <?xml version='1.0' encoding='ISO-8859-1'?>
   <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
     <SOAP-ENV:Body>
       <m:SubscribeResponse xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
       </m:SubscribeResponse>
     </SOAP-ENV:Body>
   </SOAP-ENV:Envelope>
   ```

## 登録解除(nms:購読) {#unsubscribe--nms-subscription-}

このサービスを使用すると、情報サービスから受信者を登録解除し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 登録解除するサービスの内部名、
* 受信者ドキュメント(「nms:受信者」スキーマ)を含むXML情報、

「nms:購読」スキーマの「登録解除」メソッドの説明：

```
<method name="Unsubscribe" static="true">
  <parameters>
    <param name="serviceName" type="string" desc="List of information service names (comma separated)"/>
    <param name="recipient" type="DOMElement"  desc="Recipient"/>
  </parameters>
</method>
```

紐付けキーの定義は、XMLドキュメントの `<recipient>` 要素の_key属性を介して入力する必要があります。 この属性の内容は、コンマ区切りのXPathリストです。

受信者がデータベース内に存在しない場合、または該当する情報サービスに登録されていない場合、サービスは何も行わず、エラーを生成しません。

>[!NOTE]
>
>サービス名をパラメーターとして指定しない場合、受信者は自動的にブロックリスト上(@ブロックリスト=&quot;1&quot;)に表示されます。

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

応答:

```
<?xml version='1.0' encoding='ISO-8859-1'?>
<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
  <SOAP-ENV:Body>
    <m:UnsubscribeResponse xmlns:m='urn:nms:subscription' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
    </m:UnsubscribeResponse>
  </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## SubmitDelivery(nms:配信) {#submitdelivery--nms-delivery-}

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

入力XMLドキュメントは、「nms:配信」スキーマの構造に従う配信テンプレートフラグメントです。 配信テンプレート内で静的に定義できない追加のデータ(例えば、ターゲットに対する受信者のリスト)がすべて含まれます。

この呼び出しは、エラー以外のデータを返しません。

### XMLドキュメントの例 {#xml-document-example}

この例は、外部データソース（この場合はファイル）からのカスタム配信テンプレートに基づいています。 設定は配信テンプレートで完全に説明されているので、呼び出しが発生した場合に残るのは `<externalsource>` 要素からのファイルの内容だけです。

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

