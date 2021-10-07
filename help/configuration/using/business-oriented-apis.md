---
product: campaign
title: ビジネス指向の API
description: ビジネス指向の API
audience: configuration
content-type: reference
topic-tags: api
exl-id: e6638870-3141-4f12-b904-db436127c0d1
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 4%

---

# ビジネス指向の API{#business-oriented-apis}

![](../../assets/v7-only.svg)

ビジネス API は、各タイプのオブジェクトに固有です。 以下に影響します。

* 配信:

   * 配信アクションの作成 ([SubmitDelivery (nms:delivery)](#submitdelivery--nms-delivery-) を参照 )
   * キャンペーンの送信（開始、一時停止、停止、配達確認の送信）
   * 配信ログのリカバリ

* ワークフロー:

   * ワークフローの開始
   * プロセスの検証等

      [JavaScript の SOAP メソッド ](../../configuration/using/soap-methods-in-javascript.md) を参照してください。

* コンテンツ管理
* 購読管理については、[ 購読 (nms:subscription)](#subscribe--nms-subscription-) および [ 購読解除 (nms:subscription)](#unsubscribe--nms-subscription-) を参照してください。
* データプロセス：インポート、エクスポート。

この節では、「購読」、「購読解除」および「SubmitDelivery」サービスの使用について詳しく説明します。

>[!IMPORTANT]
>
>[Campaign JSAPI ドキュメ](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html) ントには、Adobe Campaignでの SOAP 呼び出しと JavaScript の使用に関する追加情報と、アプリケーションで使用されるすべてのメソッドと関数への完全なリファレンスが含まれています。

## 購読 (nms:subscription) {#subscribe--nms-subscription-}

このサービスを使用すると、受信者を情報サービスに登録し、受信者のプロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* サブスクリプションサービスの内部名
* （「nms:recipient」スキーマの）受信者情報を含む XML ドキュメント
* 受信者の作成用のブール値（まだ存在しない場合）。

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

紐付けキーの定義は、XML ドキュメントの `<recipient>` 要素の_**key** 属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りの XPath リストです。

この呼び出しは、エラーを除き、データを返しません。

### 例 {#examples}

E メールアドレスの受信者紐付けキーを含む購読：入力 XML ドキュメントは、電子メールアドレスと、このフィールドのキーの定義を参照する必要があります。

```
<recipient _key="email" email= "john.doe@adobe.com"/>
```

受信者と購読を更新します。

```
<recipient _key="email, [folder-id]" email= "john.doe@adobe.com" folder-id="1305" firstName="John" lastName="Doe"/>
```

### SOAP メッセージの例 {#example-of-soap-messages}

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

## 購読解除 (nms:subscription) {#unsubscribe--nms-subscription-}

このサービスを使用すると、情報サービスから受信者を購読解除し、受信者プロファイルを更新できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 購読解除するサービスの内部名
* （「nms:recipient」スキーマの）受信者情報を含む XML ドキュメント

「nms:subscription」スキーマの「Unsubscribe」メソッドの説明：

```
<method name="Unsubscribe" static="true">
  <parameters>
    <param name="serviceName" type="string" desc="List of information service names (comma separated)"/>
    <param name="recipient" type="DOMElement"  desc="Recipient"/>
  </parameters>
</method>
```

紐付けキーの定義は、XML ドキュメントの `<recipient>` 要素の_key 属性を使用して入力する必要があります。 この属性の内容は、コンマ区切りの XPath リストです。

受信者がデータベースに存在しない場合や、該当する情報サービスを購読していない場合、サービスは何も実行せず、エラーは生成されません。

>[!NOTE]
>
>サービス名がパラメーターとして指定されていない場合、受信者はブロックリスト自動的に (@blackList=&quot;1&quot;) に送信されます。

この呼び出しは、エラーを除き、データを返しません。

### SOAP メッセージの例 {#example-of-soap-messages-1}

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

## SubmitDelivery (nms:delivery) {#submitdelivery--nms-delivery-}

このサービスでは、配信アクションを作成して送信できます。

サービスを呼び出すには、次のパラメーターが必要です。

* 認証
* 配信テンプレートの内部名
* 追加の配信データを含むオプションの XML ドキュメント。

パフォーマンスの問題が発生する可能性があるので、この API はボリューム内で呼び出さないでください。

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

入力 XML ドキュメントは、「nms:delivery」スキーマの構造に従う配信テンプレートフラグメントです。 配信テンプレートで静的に定義できなかったすべての追加データ（ターゲットとする受信者のリストなど）が含まれます。

この呼び出しは、エラーを除き、データを返しません。

### XML ドキュメントの例 {#xml-document-example}

この例は、外部データソース（この場合はファイル）のカスタム配信テンプレートに基づいています。 この設定は配信テンプレートで完全に説明されているので、呼び出しが発生しても送信されないのは `<externalsource>` 要素からのファイルの内容だけです。

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
