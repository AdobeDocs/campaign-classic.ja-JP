---
solution: Campaign Classic
product: campaign
title: JavaScript での SOAP メソッド
description: JavaScript での SOAP メソッド
audience: configuration
content-type: reference
topic-tags: api
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 9%

---


# JavaScript での SOAP メソッド{#soap-methods-in-javascript}

これは、Adobe Campaignサーバー上で実行されるJavaScriptです。

## 静的メソッド{#static-methods}

静的SOAPメソッドにアクセスするには、スキーマを表すオブジェクトのメソッドを呼び出します。 スキーマは、「名前空間」オブジェクトのプロパティです。 これらの名前空間はグローバル変数なので、例えばxtkやnms変数は対応する名前空間を表します

次の例は、xtk:workflowスキーマーの静的PostEventメソッドを呼び出します。

```
xtk.workflow.PostEvent("WKF1", "signal", "", $recipient-id='123', false) 
```

## 非静的メソッド{#non-static-methods}

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

