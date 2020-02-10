---
title: JavaScriptでのSOAPメソッド
seo-title: JavaScriptでのSOAPメソッド
description: JavaScriptでのSOAPメソッド
seo-description: null
page-status-flag: never-activated
uuid: 8fd1aabc-e51a-433d-835f-6b5a717c7aeb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 815d3eb9-ac45-441f-9a5f-0cd505fcf88a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# JavaScriptでのSOAPメソッド{#soap-methods-in-javascript}

これは、Adobe Campaignサーバー上で実行されるJavaScriptです。

## 静的メソッド {#static-methods}

静的SOAPメソッドには、スキーマを表すオブジェクトのメソッドを呼び出してアクセスします。 スキーマは&#39;namespace&#39;オブジェクトのプロパティです。 これらの名前空間はグローバル変数なので、例えばxtkやnms変数は対応する名前空間を表します

次の例は、xtk:workflowスキーマの静的PostEventメソッドを呼び出します。

```
xtk.workflow.PostEvent("WKF1", "signal", "", $recipient-id='123', false) 
```

## 非静的メソッド {#non-static-methods}

非静的SOAPメソッドを使用するには、まず対応するスキーマで「get」メソッドまたは「create」メソッドを使用してエンティティを取得する必要があります。

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

* 「get」操作を使用して受信者テーブルに対するクエリを実行します。

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

* 受信者テーブルにデータを書き込み中：

   ```
   xtk.session.Write(<recipient _operation="insert" lastName="Martinez" firstName="Peter" xtkschema="nms:recipient"/>);
   ```

