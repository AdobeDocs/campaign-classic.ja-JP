---
product: campaign
title: JavaScript での SOAP メソッド
feature: Configuration, Instance Settings
description: JavaScript での SOAP メソッド
role: Developer
exl-id: 62020447-fe59-4363-994d-de4d8032bbd7
TQID: https://experienceleague.adobe.com/pIvm36kXpJEzeG4mugpR-7kAQDJpyJ2YFXp4S9J7lUw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 136
ht-degree: 9%

---

# JavaScript での SOAP メソッド{#soap-methods-in-javascript}

これは、Adobe Campaign サーバーで実行されるJavaScriptです。

## 静的メソッド {#static-methods}

静的SOAP メソッドにアクセスするには、スキーマを表すオブジェクトでメソッドを呼び出します。 スキーマは、「名前空間」オブジェクトのプロパティです。 これらの名前空間はグローバル変数であるため、例えばxtkまたはnms変数は、対応する名前空間を表します

次の例では、xtk:workflow スキーマの静的PostEvent メソッドを呼び出します。

```
xtk.workflow.PostEvent("WKF1", "signal", "", $recipient-id='123', false) 
```

## 非静的メソッド {#non-static-methods}

非静的SOAP メソッドを使用するには、まず、対応するスキーマの「get」または「create」メソッドを使用してエンティティを取得する必要があります。

次の例では、「xtk:queryDef」スキーマのExecuteQuery メソッドを呼び出します。

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

* 「get」操作を使用した受信者テーブルのクエリ：

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

* 「選択」操作を使用した受信者テーブルのクエリ：

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
