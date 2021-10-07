---
product: campaign
title: JavaScript での SOAP メソッド
description: JavaScript での SOAP メソッド
audience: configuration
content-type: reference
topic-tags: api
exl-id: 62020447-fe59-4363-994d-de4d8032bbd7
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 9%

---

# JavaScript での SOAP メソッド{#soap-methods-in-javascript}

![](../../assets/v7-only.svg)

これは、Adobe Campaignサーバーで実行される JavaScript です。

## 静的メソッド {#static-methods}

静的 SOAP メソッドは、スキーマを表すオブジェクトのメソッドを呼び出すことでアクセスされます。 スキーマは、「名前空間」オブジェクトのプロパティです。 これらの名前空間はグローバル変数なので、例えば xtk や nms 変数は対応する名前空間を表します

次の例では、xtk:workflow スキーマの静的 PostEvent メソッドを呼び出します。

```
xtk.workflow.PostEvent("WKF1", "signal", "", $recipient-id='123', false) 
```

## 非静的メソッド {#non-static-methods}

非静的 SOAP メソッドを使用するには、まず対応するスキーマで「get」または「create」メソッドを使用してエンティティを取得する必要があります。

次の例では、「xtk:queryDef」スキーマの ExecuteQuery メソッドを呼び出します。

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

* 「get」操作を使用した受信者テーブルに対するクエリ：

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

* 「選択」操作を使用した受信者テーブルに対するクエリ：

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
