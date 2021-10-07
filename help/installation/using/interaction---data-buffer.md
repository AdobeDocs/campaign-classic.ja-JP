---
product: campaign
title: インタラクション - データバッファ
description: インタラクション - データバッファ
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 7250b885-0606-466a-bfc2-6dd3cc5a012d
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 17%

---

# インタラクション - データバッファ{#interaction-data-buffer}

![](../../assets/v7-only.svg)

データバッファゾーンを設定すると、オファー提案の計算が非同期化され、インバウンドインタラクションのパフォーマンスを向上できます。この設定は、インスタンス自体の設定ファイル（config-Instance.xml）で実行できます。

Adobe Campaignでは、インタラクションモジュールに **データバッファゾーン** が導入されました。 これにより、在庫とオファーの計算の非同期化により、インバウンドインタラクションのパフォーマンス **を向上させることができます。**

インバウンドインタラクション（呼び出しデータの有無に関わらず）、ステータス更新 (updateStatus) のいずれに関する場合でもかまいません。

受信者に関連する提案を書き込む際にキューを避けるため、新しい w プロセスは、**非同期で書き込む** データバッファゾーン **を生成します。**&#x200B;このデータバッファゾーンは定期的に読み出され空にされる。 デフォルトの期間は約 1 秒のスペースにあります。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファゾーン **設定** は、インスタンスの設定ファイル (config-Instance.xml) で実行できます。

>[!CAUTION]
>
>一部の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合です。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。
>
>設定に変更を加えるには、Web サーバー (Apache:IIS) とAdobe Campaignプロセスを再起動する必要があります。\
>データバッファゾーンを設定した後、適応したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。


データバッファゾーンを設定した後、適応したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。

書き込みデーモン ( プロセス名：インタラクション ) は次のとおりです。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

インバウンドインタラクションを使用する場合、 @autostart属性を「true」に設定して、Adobe Campaignサーバーが起動したときにプロセスを自動的に起動する必要があります。

引数の詳細：

```
 args: Start-up parameters 
 autoStart: Automatic start Default: false 
 callDataSize: Max. number of characters stored in the shared memory for call data
 Default: 0 
 initScript: ID of JavaScript to execute when starting the process 
 maxProcessMemoryAlertMb: Alert concerning the amount of RAM consumed (in Mb) by a given process Default: 1800 
 maxProcessMemoryWarningMb: Warning concerning the amount of RAM consumed (in Mb) by a given process Default: 1600 
 maxSharedEntries: Max. number of events stored in the shared memory. Default: 25000 
 nextOffersSize: Maximum number of eligible offers sorted right after propositions, to be stored for statistics Default: 0 
 processRestartTime: Time of the day when the process is automatically restartedDefault: '06:00:00' 
 runLevel: Priority at start Default: 10 
 targetKeySize: Max. number of characters stored in the shared memory for identifying individuals Default: 16 
```
