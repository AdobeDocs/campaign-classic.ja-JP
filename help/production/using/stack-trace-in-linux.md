---
title: Linux でのスタックトレース
seo-title: Linux でのスタックトレース
description: Linux でのスタックトレース
seo-description: null
page-status-flag: never-activated
uuid: d839df47-902f-4b92-bc78-536fc4fb6c98
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 60f306ea-4593-4e56-896e-8933277ee26a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 14%

---


# Linux でのスタックトレース{#stack-trace-in-linux}

ス **タックトレース** は、 **コア** 型ファイルに含まれるトレースを表します。 このファイルは、マシンエラーのイベントで生成されます。 エラーの接触チャネルを識別できます。

>[!NOTE]
>
>* **コア** ・ファイルの名前は **core.`<num>`**.です。
>* **gdb - GNUデバッガは** 、マシンにインストールする必要があります。

>



Adobe Campaignのテクニカルサポートから、この **スタックトレースを要求されます**。 これを取得するには、Linuxで次のコマンドを入力します。

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

Adobe Campaignのテクニカルサポートから、特定の実行可能ファイル（アドビから提供されるファイル）を使用してこのコマンドを実行するように求められる場合があります。

この場合は、 **nlserver** をAdobe Campaignが提供する実行可能ファイルに置き換えて、次のコマンドを実行します。

```
gdb nlserver <coreFile>
```

例：

```
gdb nlserver.1823 <coreFile>
```

