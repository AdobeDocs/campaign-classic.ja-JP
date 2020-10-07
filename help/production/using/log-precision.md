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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 100%

---


# ログの精度{#log-precision}

このプロセスをすべてのAdobe Campaignモジュールに適用して、ログの精度を高めることができます。

より高いレベルのログでプロセスを再起動する必要があります。

>[!CAUTION]
>
>この手順では、このモジュールで進行中のサービスをキャンセルします。

Adobe Campaignは、次の2つのレベルのログを使用して動作できます。

1. Verbose **** モードは、標準レベルの後の最初のレベルです。 次のコマンドはアクティブにします。

   ```
   nlserver restart <MODULE_NAME> -verbose 
   ```

   エラーが実際に発生したことを確認し、通常の方法でプロセスを再起動します。

   ```
   nlserver restart <MODULE_NAME> -noconsole
   ```

1. 最大数のログを保存できる **TraceFilter** モード。 アクティブにするには、次のコマンドを使用します。

   ```
   nlserver stop <MODULE_NAME>; nlserver <MODULE_NAME> -verbose -tracefilter:*
   ```

   >[!NOTE]
   >
   >tracefilter:* ****&#x200B;を使用する場合、すべてのログタイプがアクティブ化されます。ncm, rdr, nms, jst，タイミング， wdbc, ldap, soap, xtk, xtkquery，セッション， xtkwriter，ネットワーク， pop3, inmail\
   最も役立つログの種類は次のとおりです。 **wdbc** (すべてのSQLクエリを表示)、 **soap** （すべてのSOAP呼び出しを表示）、 **ldap** (認証後にすべてのLDAPクエリを表示)、 **xtkquery** (すべてのquerydefのリストを表示)。\
   これらは個別に使用できます(**例えば、tracefilter:soap,wdbc** )。 また、すべてをアクティブ化し、特定の他を除外するように選択することもできます。 **-tracefilter:*,!soap**

   エラーが実際に発生したことを確認し、通常の方法でプロセスを再起動します。

   ```
   nlserver restart <MODULE_NAME> -noconsole
   ```

>[!CAUTION]
これらのコマンドのログは、モジュールのログファイルに保存されます。

Webモジュールに固有の例を以下に示します。 他のモジュールは、上記のように動作します。

このコマンドを送信する前に、進行中のジョブが影響を受けないことを確認します。

```
nlserver pdump -who
```

次に、TraceFilter **** モードでモジュールをシャットダウンして再起動します。

```
nlserver stop web; LD_PRELOAD=libjsig.so nlserver web -tomcat -verbose -tracefilter:* -tracefile:web_debug@default
```

別の例：

```
nlserver stop mta@<INSTANCE_NAME>; nlserver mta -instance:<INSTANCE_NAME> -tracefilter:* -tracefile:mta_debug@<INSTANCE_NAME>
```

>[!NOTE]
トレー **スファイル** ・モードでは、ログを保存できます。 上記の例では、ログは **var//mta_debug.log`<instance-name>`ファイルとvar/default/web_debug.log****** ファイルに保存されます。

>[!CAUTION]
Windowsでは、LD_PRELOADオプションを追加しないでください。 次のコマンドで十分です。\
nlserver web -tomcat -verbose -tracefilter:*

問題が再度発生することを確認し、モジュールを再起動します。

```
nlserver restart web -tomcat -noconsole
```

すべての情報は、/usr/local/neolane/nl6/var/default/log/web.logファイル **で確認できます**。
