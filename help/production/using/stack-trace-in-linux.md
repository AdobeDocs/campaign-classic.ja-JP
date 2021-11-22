---
product: campaign
title: Linux でのスタックトレース
description: Linux でのスタックトレース
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 91662d6d-2177-4440-b31f-7b031bd953cb
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

---

# Linux でのスタックトレース{#stack-trace-in-linux}

![](../../assets/v7-only.svg)

A **スタックトレース** に含まれる痕跡を表す **コア** ファイルを入力します。 このファイルは、マシンエラーが発生した場合に生成されます。 エラーの発生元を識別できます。

>[!NOTE]
>
>* A **コア** ファイル名は **コア。`<num>`**.
>* **gdb - GNU デバッガ** は、コンピューターにインストールする必要があります。

>


Adobe Campaignテクニカルサポートから、 **スタックトレース**. これを取得するには、Linux で次のコマンドを入力します。

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

Adobe Campaignのテクニカルサポートから、特定の実行可能ファイル（アドビから提供される）を使用してこのコマンドを実行するように求められる場合があります。

この場合、次のコマンドを実行し、 **nlserver** Adobe Campaignが提供する実行可能ファイルを使用：

```
gdb nlserver <coreFile>
```

例：

```
gdb nlserver.1823 <coreFile>
```
