---
product: campaign
title: インタラクション - データバッファ
description: インタラクション - データバッファ
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 7250b885-0606-466a-bfc2-6dd3cc5a012d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 17%

---

# インタラクション - データバッファ{#interaction-data-buffer}

データバッファゾーンを設定すると、オファー提案の計算が非同期化され、インバウンドインタラクションのパフォーマンスを向上できます。この設定は、インスタンス自体の設定ファイル（config-Instance.xml）で実行できます。

Adobe Campaignでは、インタラクションモジュールに&#x200B;**データバッファゾーン**&#x200B;が導入されました。 これにより、在庫とオファーの計算の同期を解除して、インバウンドインタラクションのパフォーマンス&#x200B;**を向上させることができます。**

呼び出し（呼び出しデータの有無）、ステータス更新(updateStatus)のいずれによっても、インバウンドインタラクションのみが対象となります。

受信者に関連する提案を書き込む際にキューを避けるため、新しいwプロセスは、提案を&#x200B;**非同期で**&#x200B;書き込む&#x200B;**データバッファゾーン**&#x200B;を生成します。 このデータ・バッファ・ゾーンは定期的に読み出され空にされる。 デフォルトの期間は約1秒のスペース内にあります。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファゾーン&#x200B;**設定**&#x200B;は、インスタンスの設定ファイル(config-Instance.xml)で実行できます。

>[!CAUTION]
>
>一部の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合などです。 様々なデプロイメントの詳細については、[モデルのホスティング](../../installation/using/hosting-models.md)の節または[このページ](../../installation/using/capability-matrix.md)を参照してください。
>
>設定に変更を加えた場合は、Webサーバー(Apache:IIS)とAdobe Campaignプロセスを再起動する必要があります。\
>データバッファゾーンを設定した後、適応したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。


データバッファゾーンを設定した後、適応したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。

書き込みデーモン(プロセス名：インタラクション)は次のとおりです。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

インバウンドインタラクションを使用する場合、Adobe Campaignサーバーが起動したときにプロセスを自動的に起動するには、 @autostart属性を「true」にする必要があります。

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
