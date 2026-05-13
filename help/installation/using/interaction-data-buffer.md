---
product: campaign
title: インタラクション – データバッファ
description: インタラクション – データバッファ
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 7250b885-0606-466a-bfc2-6dd3cc5a012d
TQID: https://experienceleague.adobe.com/VzejoXfvy4j-bthB0FrSB-iSipA-oGLd0BmqP2niNrg
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 14%

---

# インタラクション – データバッファ{#interaction-data-buffer}



データバッファゾーンを設定すると、オファー提案の計算が非同期化され、インバウンドインタラクションのパフォーマンスを向上できます。 この設定は、インスタンス自体の設定ファイル（config-Instance.xml）で実行できます。

Adobe Campaignでは、**データバッファーゾーン**&#x200B;がインタラクションモジュールに導入されました。 これにより、在庫とオファーの計算を同期解除することで、インバウンドインタラクションのパフォーマンス **を**&#x200B;向上させることができます。

これは、呼び出し（コールデータの有無にかかわらず）またはステータス更新（updateStatus）によるインバウンドインタラクションにのみ関係します。

受信者に関連する提案を書き込む際にキューを回避するために、新しいw プロセスでは、提案を非同期で&#x200B;**書き込むことができる** データバッファーゾーン **が生成されます**。 このデータバッファーゾーンは定期的に読み取られ、空になります。 デフォルトの期間は、約1秒のスペースです。したがって、提案書はグループ化されています。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファーゾーン **設定**&#x200B;は、インスタンスの設定ファイル（config-Instance.xml）で実行できます。

>[!CAUTION]
>
>一部の設定は、Adobeがホストするデプロイメントに対してのみAdobeで実行できます。 例えば、サーバーとインスタンスの設定ファイルにアクセスする場合などです。 様々なデプロイメントについて詳しくは、[&#x200B; ホスティングモデル &#x200B;](../../installation/using/hosting-models.md) セクションまたは[このページ &#x200B;](../../installation/using/capability-matrix.md)を参照してください。
>
>設定を変更するには、Web サーバー（Apache:IIS）とAdobe Campaign プロセスを再起動する必要があります。\
>データバッファーゾーンを設定した後、適応ハードウェア設定が使用可能であることを確認してください。 （存在するメモリ量）。


データバッファーゾーンを設定した後、適応ハードウェア設定が使用可能であることを確認してください。 （存在するメモリ量）。

書き込みデーモン（プロセス名：インタラクション）の定義は次のとおりです。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

インバウンドインタラクションを使用する場合、Adobe Campaign サーバーの起動時にプロセスを自動的に起動するには、@autostart属性が「true」である必要があります。

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
