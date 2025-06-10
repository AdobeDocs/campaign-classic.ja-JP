---
product: campaign
title: 新しい GCM ベースの関数
description: 新しい GCM ベースの関数
feature: Technote
exl-id: 154dee7a-a1e9-40a2-bfa5-3641382d0574
source-git-commit: b6d64f66d287dba79be5eddec48ee852c2c7740c
workflow-type: ht
source-wordcount: '578'
ht-degree: 100%

---

# GCM ベースの関数 {#new-functions}

セキュリティを強化するために、暗号化操作に対する CBC（Cipher Block Chaining）モードでの AES（Advanced Encryption Standard）アルゴリズムの使用を非推奨にしました。新しい暗号化関数が導入されました。これらの関数では、Galois/Counter Mode を使用した AES（AES-GCM）を使用し、より安全な代替手段を提供します。これらの関数は JavaScript、JSP、SOAP API および XML スキーマで使用できるので、お客様は暗号化と復号化のために CBC から GCM に移行できます。

このドキュメントでは、新しく導入された AES-GCM 関数と非推奨（廃止予定）の CBC ベースの関数を一覧表示します。

新しい関数：

* [EncryptString API 関数](#encryptString-api-xtk)
* [EncryptStringWithServerPassword API 関数](#EncryptStringWithServerPassword-api-xtk)
* [encryptString javascript 関数](#encryptString-javascript)

GCM に使用できるレガシー関数：

* [DecryptString javascript 関数](#decryptString-javascript)
* [DecryptPassword javascript 関数](#decryptPassword-javascript)

[非推奨（廃止予定）の関数](#depracated-functions)

## API 関数

### EncryptString {#encryptString-api-xtk}

GCM モードの AES アルゴリズムを使用して、インスタンスキーで文字列を暗号化します。

```
            String 
            encrypted = EncryptString (
            String       
            decrypted
            

      )
         
```

**パラメーター**：復号化されたテキスト

**戻り値**：暗号化されています

**スキーマ**：xtk:session

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

**パラメーター**：復号化されています

**戻り値**：暗号化されています

**スキーマ**：xtk:session

**静的**：はい

## JavaScript 関数

### encryptString() {#encryptString-javascript}

インスタンスのキーまたはその他のキーを使用して、文字列を暗号化します。

```
            encryptString (str [, key
      ] [, useSalt ])
         
```

**パラメーター**：

* str：暗号化する文字列。
* key：AES 暗号化キーは、Base 64 でエンコードされます。キーの長さが 32 の場合は 256 ビット、キーの長さが 24 の場合は 192 ビット、キーの長さが 16 の場合またはキーが指定されていない場合は 128 ビットです。
* useSalt：データのソルトを使用して暗号化します。デフォルトでは True です。

**戻り値**：暗号化された文字列を返します。

**備考**

暗号化は、次の方法に従って行われます。

* Unicode 文字列は、UTF-8 文字列に変換されます。
* 暗号文の末尾にチェック文字が追加されます。
* この文字列は、12 バイトの初期化ベクターと 16 バイトのタグを持つソルトを使用して、Galois/Counter Mode（GCM）モードの AES アルゴリズムを使用して暗号化されます。パラメーターとしてキーが指定されていない場合は、インスタンスキーが使用されます。
* 暗号文には、タグと初期化ベクターが含まれます。
* 暗号化されたブロックは、Base 64 に変換されます。

復号化は、decryptString 関数を使用して実行されます。

**機能**

次で使用可能：

* コンテンツ管理
* 配信プロパティ
* 配信メッセージ
* タイポロジルール
* 読み込み
* JSSP
* SOAP メソッド
* Web アプリ
* ワークフロー

### decryptString() {#decryptString-javascript}

インスタンスのキーまたはその他のキーを使用して、文字列を復号化します。このレガシー関数は、GCM で使用できます。AES-CBC モードを使用して暗号化された暗号テキストの復号化には非推奨です。

```
            decryptString (str [, key
      ] [, useSalt ])
         
```

**パラメーター**：

* str：復号化する文字列。
* key：AES 暗号化キーは、Base 64 でエンコードされます。キーの長さが 32 の場合は 256 ビット、キーの長さが 24 の場合は 192 ビット、キーの長さが 16 の場合またはキーが指定されていない場合は 128 ビットです。
* useSalt：データのソルトを使用して復号化します。デフォルトでは True です。

**戻り値**：復号化された文字列を返します。

**警告**：データベースに保存されたパスワード（オプション／外部アカウント）は、このメソッドを使用しても復号化できません。この場合は、[decryptPassword](#decryptPassword-javascript) を使用します。

### decryptPassword() {#decryptPassword-javascript}

外部アカウントに保存されているパスワードを復号化します。このレガシー関数は、GCM で使用できます。AES-CBC モードを使用して暗号化された暗号テキストの復号化には非推奨です。

```
            decryptPassword (str)
         
```

**パラメーター**：

* str：復号化する文字列。

**戻り値**：プレーンテキストのパスワードを返します。

**備考**

この関数は、ワークフロー、web アプリケーション、レポート、配信では呼び出すことができません。JSSP または SOAP 呼び出し実装では、呼び出すことができます。例：

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

## 非推奨（廃止予定）の関数 {#depracated-functions}

次の関数は、完全に非推奨（廃止予定）になりました。

* cryptString
* Encrypt
* EncryptServerPassword
