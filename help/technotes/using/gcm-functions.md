---
product: campaign
title: 新しい GCM ベースの関数
description: 新しい GCM ベースの関数
feature: Technote
source-git-commit: b8a6a0db27826309456c285c08d4f1d85de70283
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 2%

---

# GCM ベースの関数 {#new-functions}

セキュリティを強化するため、CBC （Cipher Block Chaining）モードの AES （Advanced Encryption Standard）アルゴリズムを暗号演算に使用することを廃止しました。 新しい暗号化機能が導入されました。 これらの関数は、ガロア/カウンターモード（AES-GCM）の AES を使用して、より安全な代替手段を提供します。 これらの関数は、JavaScript、JSP、SOAP API および XML スキーマで使用でき、暗号化と復号化のために CBC から GCM に移行できます。

このドキュメントでは、新しく導入された AES-GCM 関数と、非推奨（廃止予定）になっている CBC ベースの関数を示します。

新しい関数

* [EncryptString API 関数](#encryptString-api-xtk)
* [EncryptStringWithServerPassword API 関数](#EncryptStringWithServerPassword-api-xtk)
* [encryptString javascript 関数](#encryptString-javascript)

GCM に使用できるレガシー関数：

* [DecryptString javascript 関数](#decryptString-javascript)
* [DecryptPassword JavaScript 関数](#decryptPassword-javascript)

[非推奨の関数](#depracated-functions)

## API 関数

### EncryptString {#encryptString-api-xtk}

GCM モードの AES アルゴリズムを使用して、インスタンスキーの文字列を暗号化します。

```
            String 
            encrypted = Encrypt (
            String       
            decrypted
            

      )
         
```

**パラメーター**：復号化されたテキスト

**戻り値**：暗号化されています

**スキーマ**: xtk:session

**静的**：はい

## EncryptStringWithServerPassword {#EncryptStringWithServerPassword-api-xtk}

GCM モードの AES アルゴリズムを使用して、サーバーキーで文字列を暗号化します。


```
            String 
            encrypted = EncryptStringWithServerPassword (
            String       
            decrypted
            

      )
         
```

**パラメーター**：復号化されました

**戻り値**：暗号化されています

**スキーマ**: xtk:session

**静的**：はい

## JavaScript 関数

### encryptString （） {#encryptString-javascript}

インスタンスのキーまたはその他のキーを使用して文字列を暗号化します。

```
            cryptString (str [, key
      ] [, useSalt ])
         
```

**パラメーター**:

* str：暗号化する文字列。
* key: AES 暗号化キーは base 64 でエンコードされます。キーの長さが 32 の場合は 256 ビット、キーの長さが 24 の場合は 192 ビット、キーの長さが 16 の場合またはキーが指定されていない場合は 128 ビットです。
* useSalt：暗号化するデータのソルトを使用します。 デフォルトでは true です。

**戻り値**：暗号化された文字列を返します。

**備考**

暗号化は、次の方法で行われます。

* Unicode 文字列は UTF-8 文字列に変換されます。
* 最後にチェック文字が暗号文に追加されます。
* この文字列は、12 バイトの初期化ベクトルと 16 バイトのタグを持つソルトを使用して、Galois/Counter Mode （GCM）モードの AES アルゴリズムを使用して暗号化されます。 キーがパラメーターとして指定されていない場合、インスタンスキーが使用されます。
* 暗号文には、タグと初期化ベクトルが含まれます。
* 次に、暗号化されたブロックがベース 64 に変換されます。

復号化は、decryptString 関数を使用して実行されます。

**機能**

次の場所で使用可能：

* コンテンツ管理
* 配信プロパティ
* 配信メッセージ
* タイポロジルール
* 読み込み
* JSSP
* SOAPの手法
* Web アプリ
* ワークフロー

### decryptString （） {#decryptString-javascript}

インスタンスのキーまたはその他のキーを使用して文字列を暗号化します。 このレガシー関数は、GCM で使用できます。 AES-CBC モードを使用して暗号化された暗号テキストの復号化のために非推奨です。

```
            decryptString (str [, key
      ] [, useSalt ])
         
```

**パラメーター**:

* str：復号する文字列。
* key: AES 暗号化キーは base 64 でエンコードされます。キーの長さが 32 の場合は 256 ビット、キーの長さが 24 の場合は 192 ビット、キーの長さが 16 の場合またはキーが指定されていない場合は 128 ビットです。
* useSalt：復号化するデータのソルトを使用します。 デフォルトでは true です。

**戻り値**：復号化された文字列を返します。

**警告**：このメソッドを使用すると、データベースに保存されているパスワード（オプション /外部アカウント）を復号化できなくなりました。 その場合は、[decryptPassword](#decryptPassword-javascript) を使用します。

### decryptPassword （） {#decryptPassword-javascript}

外部アカウントに保存されているパスワードを復号化します。 このレガシー関数は、GCM で使用できます。 AES-CBC モードを使用して暗号化された暗号テキストの復号化のために非推奨です。

```
            decryptPassword (str)
         
```

**パラメーター**:

* str：復号する文字列。

**戻り値**：プレーンテキストのパスワードを返します。

**備考**

この関数は、ワークフロー、web アプリケーション、レポート、配信では呼び出すことができません。 JSSP またはSOAPの呼び出し実装で呼び出すことができます。 例：

```
        function nms_extAccount_LogonToRemoteInstance(remoteInstanceUrl, login, encryptedPassword) {
        var cnx = null, sessionService = null;
        try
            {
                var cnx = new HttpSoapConnection(remoteInstanceUrl + '/nl/jsp/soaprouter.jsp', 'utf-8', 0);
                sessionService = new SoapService(cnx, 'xtk:session');
                sessionService.addMethod("Logon", "xtk:session#Logon",
                    ["token", "string", "login", "string", "password", "string", "parameters", "NLElement"],
                    ["sessionToken", "string", "sessionInfo", "NLElement", "securityToken", "string"]);
                return sessionService.Logon("", login, decryptPassword(encryptedPassword), <parameters/>);
            }
        catch( e ) {
        logError(e);
        }
        finally {
        if( sessionService ) sessionService.dispose();
        if( cnx ) cnx.dispose();
        }
        })
      
```

## 非推奨の関数 {#depracated-functions}

次の関数は完全に非推奨（廃止予定）です。

* cryptString
* 暗号化
* EncryptServerPassword
