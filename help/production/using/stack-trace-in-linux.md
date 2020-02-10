---
title: Linuxでのスタックトレース
seo-title: Linuxでのスタックトレース
description: Linuxでのスタックトレース
seo-description: null
page-status-flag: never-activated
uuid: d839df47-902f-4b92-bc78-536fc4fb6c98
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 60f306ea-4593-4e56-896e-8933277ee26a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9482a99c3be164651b3428179388cb0a8a75783f

---


# Linuxでのスタックトレース{#stack-trace-in-linux}

スタック **トレースは** 、コアタイプファイルに含まれるト **レース** を表します。 このファイルは、マシンエラーが発生した場合に生成されます。 エラーの原因を特定できます。

>[!NOTE]
>
>* コアフ **ァイルは** 、 **core.`<num>`**.という名前です。
>* **gdb - GNU Debuggerは** 、マシンにインストールする必要があります。
>



Adobe Campaignテクニカルサポートから、このスタックトレースを要 **求されます**。 これを取得するには、Linuxで次のコマンドを入力します。

```
su - neolane
gdb nlserver <coreFile>
//You get lots of output but the stack trace (or Back trace) can be obtained with : 
(gdb) bt
// and forward all the output : 
#0 0x0836c189 in ObjectValue::SetPropertyTarget ()
#1 0x082623b3 in CXtkScriptProperty::VDeclareProperties ()
#2 0x0826a835 in CXtkScriptContext::OnGetProperty ()
#3 0x08370b3d in JavaScriptGetProperty ()
#4 0x557b8aa7 in js_Interpret () from /usr/local/neolane/nl6/lib/libmozjs.so
#5 0x557afb97 in js_Execute () from /usr/local/neolane/nl6/lib/libmozjs.so
#6 0x5578921f in JS_ExecuteScript () from /usr/local/neolane/nl6/lib/libmozjs.so
#7 0x08370468 in JavaScriptSource::Evaluate ()
#8 0x0848fa03 in JSTDeliveryContext::ProcessScript ()
#9 0x0848fcb6 in JSTDeliveryContext::ProcessTemplate ()
#10 0x08460d2b in CDeliveryToolbox::CreateMailMessage ()
#11 0x080d51fe in CMtaQueue::PrepareMessages ()
#12 0x080d2b07 in CMtaQueue::Prepare ()
#13 0x080dca38 in CMtaChild::OnRun ()
#14 0x0814792c in ThreadStartRoutine ()
#15 0x55575b63 in start_thread () from /lib/tls/libpthread.so.0
#16 0x5565918a in clone () from /lib/tls/libc.so.6
```

Adobe Campaignテクニカルサポートから、特定の実行可能ファイル（アドビから提供されるファイル）を使用してこのコマンドを実行するように求められる場合があります。

この場合は、 **nlserver** をAdobe Campaignが提供する実行可能ファイルに置き換えて、次のコマンドを実行します。

```
gdb nlserver <coreFile>
```

次に例を示します。

```
gdb nlserver.1823 <coreFile>
```

