---
product: campaign
title: ログの精度
description: ログの精度
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: c2470098-62f3-4fee-b1c5-800ed0e91f75
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 79%

---

# ログの精度{#log-precision}



このプロセスをすべてのAdobe Campaignモジュールに適用して、ログの精度を高めることができます。

より高いレベルのログでプロセスを再起動する必要があります。

>[!IMPORTANT]
>
>この手順では、このモジュールで進行中のサービスをキャンセルします。

Adobe Campaignは、次の2つのレベルのログを使用して動作できます。

1. Verbose **&#x200B;**&#x200B;モードは、標準レベルの後の最初のレベルです。 次のコマンドはアクティブにします。

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
   >**tracefilter:&#42;** を使用すると、すべてのログタイプ（ncm、rdr、nms、jst、タイミング、wdbc、ldap、soap、xtk、xtkquery、session、xtkwriter、network、pop3、inmail）がアクティブ化されます\
   >最も役立つログの種類は次のとおりです。 **wdbc** (すべてのSQLクエリを表示)、 **soap** （すべてのSOAP呼び出しを表示）、 **ldap** (認証後にすべてのLDAPクエリを表示)、 **xtkquery** (すべてのquerydefのリストを表示)。\
   >これらは個別に使用できます(**例えば、tracefilter:soap,wdbc** )。 また、それらをすべてアクティブにして、他の特定の除外を選択することもできます。**-tracefilter:&#42;,!soap**

   エラーが実際に発生したことを確認し、通常の方法でプロセスを再起動します。

   ```
   nlserver restart <MODULE_NAME> -noconsole
   ```

>[!IMPORTANT]
>
>これらのコマンドのログは、モジュールのログファイルに保存されます。

Webモジュールに固有の例を以下に示します。 他のモジュールは、上記のように動作します。

このコマンドを送信する前に、進行中のジョブが影響を受けないことを確認してください：

```
nlserver pdump -who
```

次に、**TraceFilter** モードでモジュールをシャットダウンして再起動します。

```
nlserver stop web; LD_PRELOAD=libjsig.so nlserver web -tomcat -verbose -tracefilter:* -tracefile:web_debug@default
```

別の例：

```
nlserver stop mta@<INSTANCE_NAME>; nlserver mta -instance:<INSTANCE_NAME> -tracefilter:* -tracefile:mta_debug@<INSTANCE_NAME>
```

>[!NOTE]
>
>トレー **スファイル** ・モードでは、ログを保存できます。 上記の例では、ログは **var//mta_debug.log`<instance-name>`ファイルとvar/default/web_debug.log**&#x200B;**&#x200B;** ファイルに保存されます。

>[!IMPORTANT]
>
>Windowsでは、LD_PRELOADオプションを追加しないでください。 次のコマンドで十分です。\
>nlserver web -tomcat -verbose -tracefilter:&#42;

問題が再度発生することを確認し、モジュールを再起動します。

```
nlserver restart web -tomcat -noconsole
```

すべての情報は、/usr/local/neolane/nl6/var/default/log/web.logファイル **で確認できます**。
