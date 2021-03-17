---
solution: Campaign Classic
product: campaign
title: インタラクション - データバッファ
description: インタラクション - データバッファ
audience: installation
content-type: reference
topic-tags: additional-configurations
translation-type: tm+mt
source-git-commit: d88815e36f7be1b010dcaeee51013a5da769b4a8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 17%

---


# インタラクション - データバッファ{#interaction-data-buffer}

データバッファゾーンを設定すると、オファー提案の計算が非同期化され、インバウンドインタラクションのパフォーマンスを向上できます。この設定は、インスタンス自体の設定ファイル（config-Instance.xml）で実行できます。

Adobe Campaignでは、**データバッファーゾーン**&#x200B;がインタラクションモジュールに導入されました。 これにより、在庫とオファーの計算を非同期化して、受信インタラクションのパフォーマンス&#x200B;**を**&#x200B;向上させることができます。

呼び出しによる操作（呼び出しデータの有無に関係なく）、またはステータス更新による操作(updateStatus)のみが考慮されます。

受信者に関する提案を書き込む際のキューを回避するために、新しいプロセスは、提案を&#x200B;**非同期で**&#x200B;書き込む&#x200B;**データバッファゾーン**&#x200B;を生成する。 このデータ・バッファ・ゾーンは定期的に読み取られ、空になる。 既定の期間は約1秒の間隔です。したがって、提案書の作成はグループ化されます。

>[!NOTE]
>
>インタラクションを分散アーキテクチャで使用する場合、これは必要不可欠なパラメーターです。

データバッファーゾーン&#x200B;**設定**&#x200B;は、インスタンスの設定ファイル(config-Instance.xml)で実行できます。

>[!CAUTION]
>
>一部の設定は、Adobeがホストする配置に対してのみAdobeが実行できます。 例えば、サーバー設定ファイルやインスタンス設定ファイルにアクセスする場合です。 各デプロイメントの詳細については、[「モデルのホスト](../../installation/using/hosting-models.md)」セクションまたは[このページ](../../installation/using/capability-matrix.md)を参照してください。
>
>設定に変更を加えた場合は、Webサーバー(Apache:IIS)を再起動し、Adobe Campaignプロセスを実行する必要があります。\
>データバッファゾーンを設定した後、適切なハードウェア設定が使用可能であることを確認してください。 （存在するメモリ量）。


データバッファゾーンを設定した後、適切なハードウェア設定が使用可能であることを確認してください。 （存在するメモリ量）。

書き込みデーモン(プロセス名：インタラクション)は、次のようになります。

```
<interactiond args="" autoStart="false" callDataSize="0" initScript="" maxProcessMemoryAlertMb="1800"
maxProcessMemoryWarningMb="1600" maxSharedEntries="25000" nextOffersSize="0"
processRestartTime="06:00:00" runLevel="10" targetKeySize="16"/>
```

受信インタラクションを使用する場合、Adobe Campaignサーバーの起動時にプロセスを自動的に起動するには、@autostart属性を「true」に設定する必要があります。

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

