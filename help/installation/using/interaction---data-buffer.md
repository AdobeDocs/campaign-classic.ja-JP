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

Adobe Campaignで、 **データバッファゾーン** は、インタラクションモジュールで導入されました。 次の操作が可能です。 **業績を上げる** インバウンドインタラクションの合計を調整します。

インバウンドインタラクションのみに関係します。呼び出し（呼び出しデータの有無）、またはステータスの更新 (updateStatus) のどちらであるかは関係ありません。

受信者に関する提案を書き込む際にキューを避けるため、新しいプロセスで **データバッファゾーン** それは提案を可能にする **非同期で書き込まれる**. このデータバッファゾーンは定期的に読み取られ、空にされます。 デフォルトの期間は約 1 秒のスペースにあります。したがって、提案書の作成はグループ化されます。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファゾーン **設定** は、インスタンスの設定ファイル (config-Instance.xml) で実行できます。

>[!CAUTION]
>
>一部の設定は、Adobeがホストするデプロイメントの場合、Adobeが実行できるだけです。 例えば、サーバーおよびインスタンスの設定ファイルにアクセスする場合です。 様々なデプロイメントについて詳しくは、 [ホスティングのモデル](../../installation/using/hosting-models.md) セクションまたは [このページ](../../installation/using/capability-matrix.md).
>
>設定に変更を加えた場合は、Web サーバー (Apache:IIS) とAdobe Campaignプロセスを再起動する必要があります。\
>データバッファゾーンを設定した後、適合したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。


データバッファゾーンを設定した後、適合したハードウェア設定が使用可能であることを確認してください。 （存在するメモリの量）。

書き込みデーモンの定義 ( プロセス名：インタラクション ) は次のようになります。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

インバウンドインタラクションを使用する場合、Adobe Campaignサーバーが起動したときにプロセスが自動的に起動されるように、 @autostart属性を「true」に設定する必要があります。

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
