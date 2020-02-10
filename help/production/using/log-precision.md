---
title: ログの精度
seo-title: ログの精度
description: ログの精度
seo-description: null
page-status-flag: never-activated
uuid: 8396bc4f-2954-40bb-b511-61802e60e123
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: c6c39b7d-7bbd-4789-b1ea-b938153e9679
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 779d9162b7296339a796512838612ede1186ddcc

---


# ログの精度{#log-precision}

このプロセスをすべてのAdobe Campaignモジュールに適用して、ログの精度を向上させることができます。

より高いレベルのログを使用してプロセスを再起動する必要があります。

>[!CAUTION]
>
>この手順は、このモジュールで処理中のサービスをキャンセルします。

Adobe Campaignは、次の2つのレベルのログを使用して操作できます。

1. 詳細モ **ードは** 、標準レベルの後の最初のレベルです。 次のコマンドはアクティブにします。

   ```
   nlserver restart <MODULE_NAME> -verbose 
   ```

   エラーが実際に発生したことを確認し、通常の方法でプロセスを再起動します。

   ```
   nlserver restart <MODULE_NAME> -noconsole
   ```

1. TraceFilter **** モード。最大数のログを保存できます。 次のコマンドでアクティブにします。

   ```
   nlserver stop <MODULE_NAME>; nlserver <MODULE_NAME> -verbose -tracefilter:*
   ```

   >[!NOTE]
   >
   >tracefilter:* **を使用すると、すべてのログタイプがアクティブになります**。ncm, rdr, nms, jst, timing, wdbc, ldap, soap, xtk, xtkquery, session, xtkwriter, network, pop3, inmail\
   最も役に立つログタイプは次のとおりです。 **wdbc** （全てのSQLクエリを表示）、 **soap** （全てのSOAP呼び出しを表示）、 **ldap （認証後にすべてのLDAPクエリを表示）、****** xtkquery xtkquery （全てのSQLクエリを表示）。\
   これらは個別に使用で&#x200B;**きます(例：tracefilter:soap,wdbc** )。 また、すべてをアクティブにし、特定の他を除外するように選択することもできます。 **-tracefilter:*,!soap**

   エラーが実際に発生したことを確認し、通常の方法でプロセスを再起動します。

   ```
   nlserver restart <MODULE_NAME> -noconsole
   ```

>[!CAUTION]
これらのコマンドのログは、モジュールのログファイルに保存されます。

以下は、Webモジュールに固有の例です。 他のモジュールは、上記の通り動作します。

このコマンドを送信する前に、進行中のジョブが影響を受けないことを確認します。

```
nlserver pdump -who
```

次に、 **TraceFilterモードでモジュールをシャットダウンし、再起動します** 。

```
nlserver stop web; LD_PRELOAD=libjsig.so nlserver web -tomcat -verbose -tracefilter:* -tracefile:web_debug@default
```

別の例：

```
nlserver stop mta@<INSTANCE_NAME>; nlserver mta -instance:<INSTANCE_NAME> -tracefilter:* -tracefile:mta_debug@<INSTANCE_NAME>
```

>[!NOTE]
トレー **スファイル** ・モードでは、ログを保存できます。 上記の例では、ログは **var//mta_debug.logファイルとvar/default/web_debug.logフ`<instance-name>`ァイル** に保存 **されます** 。

>[!CAUTION]
Windowsでは、LD_PRELOADオプションを追加しないでください。 次のコマンドで十分です。\
nlserver web - tomcat -verbose -tracefilter:*

問題が再び発生することを確認し、モジュールを再起動します。

```
nlserver restart web -tomcat -noconsole
```

すべての情報は、/usr/local/neolane/nl6/var/default/log/web.logにあり **ます**。
