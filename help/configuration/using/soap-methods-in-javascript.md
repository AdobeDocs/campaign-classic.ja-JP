---
product: campaign
title: JavaScript での SOAP メソッド
feature: Configuration, Instance Settings
description: JavaScript での SOAP メソッド
role: Developer
exl-id: 62020447-fe59-4363-994d-de4d8032bbd7
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '136'
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
