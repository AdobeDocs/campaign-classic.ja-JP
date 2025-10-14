---
product: campaign
title: インタラクション – データバッファー
description: インタラクション – データバッファー
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 7250b885-0606-466a-bfc2-6dd3cc5a012d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 14%

---

# インタラクション – データバッファー{#interaction-data-buffer}



データバッファゾーンを設定すると、オファー提案の計算が非同期化され、インバウンドインタラクションのパフォーマンスを向上できます。この設定は、インスタンス自体の設定ファイル（config-Instance.xml）で実行できます。

Adobe Campaignでは、インタラクションモジュールに **データバッファーゾーン** が導入されました。 これにより、在庫とオファーの計算の同期を解除することで、インバウンドインタラクションの **パフォーマンスの向上** が可能になります。

これは、呼び出し（呼び出しデータの有無）やステータス更新（updateStatus）のいずれを行った場合でも、インバウンドインタラクションにのみ関係します。

受信者に関連する提案を書き込む際のキューを避けるために、新しいプロセスは、提案を **非同期で書き込む** ことができる **データバッファーゾーン** を生成する。 このデータバッファーゾーンは、定期的に読み取られ、空にされる。 デフォルトの期間は約 1 秒のスペースです。したがって、提案書き込みはグループ化されます。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファーゾーン **設定** は、インスタンスの設定ファイル（config-Instance.xml）で実行できます。

>[!CAUTION]
>
>一部の設定は、Adobeがホストするデプロイメントに対してのみAdobeが実行できます。 例えば、サーバーおよびインスタンス設定ファイルにアクセスするには、次の手順を実行します。 様々なデプロイメントの詳細については、[&#x200B; モデルのホスティング &#x200B;](../../installation/using/hosting-models.md) の節または [&#x200B; このページ &#x200B;](../../installation/using/capability-matrix.md) を参照してください。
>
>設定に変更を加えた場合は、web サーバー（Apache:IIS）とAdobe Campaign プロセスを再起動する必要があります。\
>データバッファーゾーンを設定したら、適合するハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。


データバッファーゾーンを設定したら、適合するハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。

書き込みデーモン （プロセス名：インタラクション）の定義は次のとおりです。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

インバウンドインタラクションを使用する場合、Adobe Campaign サーバーの起動時にプロセスを自動的に起動するには、@autostart 属性を「true」にする必要があります。

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
