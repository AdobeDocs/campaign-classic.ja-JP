---
title: JavaScript での SOAP メソッド
seo-title: JavaScript での SOAP メソッド
description: JavaScript での SOAP メソッド
seo-description: null
page-status-flag: never-activated
uuid: 8fd1aabc-e51a-433d-835f-6b5a717c7aeb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 815d3eb9-ac45-441f-9a5f-0cd505fcf88a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# JavaScript での SOAP メソッド{#soap-methods-in-javascript}

これは、Adobe Campaignサーバー上で実行されるJavaScriptです。

## 静的メソッド {#static-methods}

静的SOAPメソッドにアクセスするには、スキーマを表すオブジェクトのメソッドを呼び出します。 スキーマは、「名前空間」オブジェクトのプロパティです。 これらの名前空間はグローバル変数なので、例えばxtkやnms変数は対応する名前空間を表します

次の例は、xtk:workflowスキーマーの静的PostEventメソッドを呼び出します。

```
xtk.workflow.PostEvent("WKF1", "signal", "", $recipient-id='123', false) 
```

## 非静的メソッド {#non-static-methods}

非静的SOAPメソッドを使用するには、まず、対応するスキーマで「get」メソッドまたは「create」メソッドを使用してエンティティを取得する必要があります。

次の例は、「xtk:queryDef」スキーマのExecuteQueryメソッドを呼び出します。

```
var query = xtk.queryDef.create(
  <queryDef schema="xtk:workflow" operation="select">
    <select>
      <node expr="@internalName"/>
    </select>
  </queryDef>
)

var res = query.ExecuteQuery()

for each (var w in res.workflow) 
  logInfo(w.@internalName)
```

## 例 {#examples}

* 「get」操作を含む受信者テーブルのクエリ:

   ```
   var query = xtk.queryDef.create(  
     <queryDef schema="nms:recipient" operation="get">    
       <select>      
         <node expr="@firstName"/>      
         <node expr="@lastName"/>      
         <node expr="@email"/>    
       </select>    
       <where>      
         <condition expr="@email = 'peter.martinez@adobe.com'"/>    
       </where>  
     </queryDef>)
   
   var recipient = query.ExecuteQuery()
   
   logInfo(recipient.@firstName)
   logInfo(recipient.@lastName)
   ```

* 「select」操作を含む受信者テーブルのクエリ:

   ```
   var query = xtk.queryDef.create(  
     <queryDef schema="nms:recipient" operation="select">    
       <select>      
         <node expr="@email"/>      
         <node expr="@lastName"/>      
         <node expr="@firstName"/>    
       </select>    
       <where>      
         <condition expr="@age > 25"/>    
       </where>    
     </queryDef>)
   
   var res = query.ExecuteQuery()
   
   for each (var recipient in res.recipient) 
   {  
     logInfo(recipient.@email)  
     logInfo(recipient.@firstName)  
     logInfo(recipient.@lastName)
   }
   ```

* 受信者テーブルへのデータの書き込み：

   ```
   xtk.session.Write(<recipient _operation="insert" lastName="Martinez" firstName="Peter" xtkschema="nms:recipient"/>);
   ```

