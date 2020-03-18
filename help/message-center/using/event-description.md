---
title: イベントの説明
seo-title: イベントの説明
description: イベントの説明
seo-description: null
page-status-flag: never-activated
uuid: 7b174ffd-28b2-4147-b992-e17b0b2cf733
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: introduction
discoiquuid: 3c8388d8-1a91-4d16-a8ac-016f643c6009
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: bc227c2da2e8b1a78714748809ad40bbcefe0458

---


# イベントの説明{#event-description}

## トランザクションメッセージングデータモデルについて {#about-transactional-messaging-datamodel}

トランザクションメッセージングは、Adobe Campaignのデータモデルに依存し、2つの別々のテーブルを使用します。 These [tables](../../configuration/using/data-model-description.md#message-center-module), **NmsRtEvent** and **NmsBatchEvent**, contain the same fields and let you manage real time events on the one hand and batch events on the other.

## SOAP メソッド {#soap-methods}

本節では、トランザクションメッセージモジュールのスキーマに関連する SOAP メソッドの詳細を説明します。

2 つの **PushEvent** または **PushEvents** SOAP メソッドは、2 つの **nms:rtEvent** と **nms:BatchEvent** データスキーマに関連付けられています。イベントのタイプが「バッチ」なのか「リアルタイム」なのかの判断は、情報システムがおこないます。

* **PushEvent** では、メッセージに 1 つのイベントを挿入することができ、
* **PushEvents** では、メッセージに一連の複数のイベントを挿入することができます。

両方のメソッドにアクセスする WSDL パスは：

* **http://hostname/nl/jsp/schemawsdl.jsp?schema=nms:rtEvent** で、リアルタイムタイプのスキーマにアクセスできます。
* **http://hostname/nl/jsp/schemawsdl.jsp?schema=nms:batchEvent** で、バッチタイプのスキーマにアクセスできます。

Both methods contain an **`<urn:sessiontoken>`** element for logging on to the transactional messaging module. 信頼済み IP アドレス経由の識別方法を使用することをお勧めします。セッショントークンを取得するには、ログオン SOAP 呼び出しを実行してから、トークンを取得した後でログオフします。同じトークンを 複数の RT 呼び出しに使用します。この節に含まれる例では、推奨されるセッショントークン方式を使用しています。

ロードバランササーバーを使用している場合は、（RT メッセージのレベルで）ユーザー／パスワード認証を使用できます。例：

```
<PushEvent xmlns="urn:nms:rtEvent">
<sessiontoken>mc/PASSWORD</sessiontoken>
<domEvent>
<rtEvent wishedChannel="41" type="rt_MobileJourney_iOS_Push" registrationToken="c3ddc8aaecc24822df25d0f49865cca61ea3f86c61bfa53ae4d37294e37f4a1c" hashlpId="27EE7571EC14DBA23B9B5CC0EF79BB782DAECF4C03C88E5D92CC9B9DAC4E5DDA" correlationId="415b7593-4f6f-e911-811f-00505691247c" xmlns="">
<mobileApp uuid="236B24DC-C073-412F-8BCB-AC7207096258" _operation="none"/>
<ctx>...</ctx>
</rtEvent>
</domEvent>
</PushEvent>
```

The **PushEvent** method is made up of a **`<urn:domevent>`** parameter which contains the event.

The **PushEvents** method is made up of a **`<urn:domeventcollection>`** parameter which contains events.

PushEvent の使用例：

```
<urn:PushEvent>

 <sessiontoken>___921f9b38-72ac-49ad-b481-ab32973efc50</sessiontoken>
 
 <urn:domEvent>
 
   <rtEvent>
   
   ...
   
   </rtEvent>
 
 </urn:domEvent>

</urn:PushEvent>
```

>[!NOTE]
>
>**PushEvents** メソッドを呼び出す場合、標準 XML に準拠するには親 XML 要素を追加する必要があります。This XML element will frame the various **`<rtevent>`** elements contained in the event.

PushEvents の使用例：

```
<urn:PushEvents>

 <sessiontoken>___921f9b38-72ac-49ad-b481-ab32973efc50</sessiontoken>
 
 <urn:domEventCollection>
 
   <Events>
   
     <rtEvent>... </rtEvent>
     
     <rtEvent>... </rtEvent>
     
     ...
   
   </Events>
 
 </urn:domEventCollection>

</urn:PushEvents>
```

要素と **`<rtevent>`** 要素 **`<batchevent>`** には、属性のセットと必須の子要素が含まれます。メッセー **`<ctx>`** ジデータの統合。

>[!NOTE]
>
>The **`<batchevent>`** element lets you add the event to the &quot;batch&quot; queue. The **`<rtevent>`** adds the event to the &quot;real time&quot; queue.

The mandatory attributes of the **`<rtevent>`** and **`<batchevent>`** elements are @type and @email. @type の値は、実行インスタンスを設定した際に定義した項目別リストの値と同じである必要があります。この値で、配信の間、イベントの内容にリンクされるテンプレートを定義できます。

`<rtevent> configuration example:`

```
<rtEvent type="order_confirmation" email="john.doe@domain.com" origin="eCommerce" wishedChannel="0" externalId="1242" mobilePhone="+33620202020"> 
```

この例では、2 つのチャネルが指定されています。E メールアドレスと携帯電話番号です。**wishedChannel** では、イベントをメッセージに変換する際に使用するチャネルを選択できます。値「0」は E メールチャネルに、「1」はモバイルチャネルに対応します。

イベントの配信を遅らせる場合には、**[!UICONTROL scheduled]** フィールドに続いて希望する日付を追加します。イベントは、指定した日付にメッセージに変換されます。

@wishedChannel と @emailFormat 属性には、数値を入力することをお勧めします。データスキーマの説明に、数値とラベルを関連付ける関数表が記載されています。

>[!NOTE]
>
>許可されているすべての属性とその値についての詳細は、**nms:rtEvent** および **nms:BatchEvent** データスキーマの説明に記載されています。

The **`<ctx>`** element contains the message data. この XML コンテンツはオープンなので、配信するコンテンツに合わせて設定できます。

>[!NOTE]
>
>配信中にサーバーに過大な負荷をかけないようにするには、メッセージに含まれる XML ノードの数とサイズを最適化することが重要です。

データ例：

```
   <ctx>
               <client>
                        <firstname>John</firstname>
                        <lastname>Doe</lastname>
               </client>
               <action>
                         <type>Order confirmation</type>
                          <number>CN23453</number>
               </action>
               <orderdetails>
                          <article num="1">
                                   <name>Generic USB key</name>
                                   <price>20</price>
                           </article>
               </orderdetails>
    </ctx>
   
```

## SOAP 呼び出しにより返される情報： {#information-returned-by-the-soap-call}

イベントを受け取ると、Adobe Campaign は一意の戻り識別子を生成します。これが、アーカイブバージョンのイベントの識別子になります。

>[!CAUTION]
>
>SOAP 呼び出しを受け取ると、Adobe Campaign は E メールアドレスの形式を検証します。E メールアドレスの形式が正しくない場合、エラーを返します。

* イベント処理が成功した場合にメソッドが返す識別子の例：

   ```
   <SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns="http://xml.apache.org/xml-soap" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
      <SOAP-ENV:Body>
         <urn:PushEventResponse SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:urn="urn:nms:rtEvent">
            <plId xsi:type="xsd:long">72057594037935966</plId>
         </urn:PushEventResponse>
      </SOAP-ENV:Body>
   </SOAP-ENV:Envelope>
   ```

戻り識別子の値が 0 より大きい数値の場合、Adobe Campaign 内でイベントのアーカイブが成功したことを意味します。

しかし、イベントの処理に失敗すると、このメソッドはエラーメッセージまたは 0 の値を返します。

* クエリにログインが含まれていない、または指定したオペレーターに必要な権限がなく、失敗したイベントの処理例：

   ```
   <SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
      <SOAP-ENV:Body>
         <SOAP-ENV:Fault>
            <faultcode>SOAP-ENV:Client</faultcode>
            <faultstring xsi:type="xsd:string">Error while reading parameters of method 'PushEvent' of service 'nms:rtEvent'.</faultstring>
            <detail xsi:type="xsd:string">Invalid login or password. Connection denied.</detail>
         </SOAP-ENV:Fault>
      </SOAP-ENV:Body>
   </SOAP-ENV:Envelope>
   ```

* クエリのエラー（XML 分類に従っていない）により失敗したイベントの例：

   ```
   <SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
      <SOAP-ENV:Body>
         <SOAP-ENV:Fault>
            <faultcode>SOAP-ENV:Client</faultcode>
            <faultstring xsi:type="xsd:string">The XML SOAP message is invalid (service 'PushEvent', method 'nms:rtEvent').</faultstring>
            <detail xsi:type="xsd:string"><![CDATA[(16:8) : Expected end of tag 'rtevent'
   Error while parsing XML string '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:nms:rtEvent">
      <soapenv:Header/>
      <soapenv:Body>
         <urn:PushEvent>
            <urn:sessiontoken>mc/</urn:sessiontoken>
            <urn:domEvent>
   <rtevent type="create_account" email="esther.hall@adobe.com" origin="eCommerce" wishedChannel="email" 
         externalId="1596" language="english" country="EN" emailFormat="2"
         mobilePhone="+447700123123">
     <ctx>
      <website name="eCommerce" url="http://www.eCo']]></detail>
         </SOAP-ENV:Fault>
      </SOAP-ENV:Body>
   </SOAP-ENV:Envelope>
   ```

* 失敗し、0 の識別子を返したイベントの例（誤ったメソッド名）：

   ```
   <SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns="http://xml.apache.org/xml-soap" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
      <SOAP-ENV:Body>
         <urn:PushEventResponse SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/" xmlns:urn="urn:nms:rtEvent">
            <plId xsi:type="xsd:long">0</plId>
         </urn:PushEventResponse>
      </SOAP-ENV:Body>
   </SOAP-ENV:Envelope>
   ```

