---
product: campaign
title: 追加の Web トラッキングパラメーター
description: Web トラッキングのパラメーターの詳細
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: d14d94fd-b078-4893-be84-31d37a1d50f5
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---

# 追加パラメーター{#additional-parameters}

![](../../assets/v7-only.svg)

## パラメーターの定義 {#definition-of-parameters}

Adobe Campaignプラットフォームでは、標準として 2 つの TRANSACTION タイプの Web トラッキングパラメーターが提供されます。

* **量**:トランザクションの金額を表します。
* **記事**:トランザクション内の品目数を表します。

これらのパラメーターは、 **nms:webTrackingLog** スキーマとは、レポートで確認できる指標の一部です。

追加のパラメーターを定義するには、このスキーマを拡張する必要があります。

**例**：

```
<srcSchema extendedSchema="nms:webTrackingLog" label="Web Tracking"
           mappingType="sql" name="webTrackingLog" 
           namespace="cus" xtkschema="xtk:srcSchema">

  <element name="webTrackingLog">
    <attribute desc="Payment method" label="Payment method" length="10" name="mode" type="string"/>
    <attribute desc="Offer code" label="Offer code" length="5" name="code" type="string"/>
  </element>
</srcSchema>
```

（配信または受信者の）トラッキングログリストを設定することで、これらのパラメーターの値を表示できます。

## リダイレクトサーバーの設定 {#redirection-server-configuration}

サーバーの設定で、Web トラッキングパラメーターで使用する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮する最大文字数を増やすと、プラットフォームの Web トラッキングのパフォーマンスに影響を与える可能性があります。

これをおこなうには、 **webTrackingParamSize** の属性 **`<trackinglogd>`** 要素を **serverConf.xml** ファイル。 このファイルは、 **conf** Adobe Campaignインストールディレクトリのサブディレクトリ。

**例**：

デフォルト値は 64 文字です。 この値では、 **量** および **記事** (&quot;amount=xxxxxxxxx&amp;article=xxxxxxxxxx&quot;) 標準パラメーター。

上記の拡張スキーマの例で示した両方のパラメーター（名前のサイズ+値のサイズ）を考慮することで、100 文字を考慮に入れるよう設定を変更できます (「amount=xxxxxxxx&amp;article=xxxxxxxx&amp;mode=xxxxxxxxxxxx&amp;code=xxxxxxx」)。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストする Web サーバー（Apache、IIS など）を停止し、
* Adobe Campaignサーバーを停止します。 **net stop nlserver6** Windows の場合、 **/etc/init.d/nlserver6 停止** Linux では、

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl stop nlserver**

* Linux では、 **ipcrm** コマンド
* Adobe Campaignサーバーを再起動します。 **net start nlserver6** Windows の場合、 **/etc/init.d/nlserver6 start** Linux では、

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver**

* Web サーバーを再起動します。

**例**:Linux での設定を考慮して

```
adobe@selma:~$ systemctl stop nlserver
adobe@selma:~$ systemctl stop apache2
adobe@selma:~$ ipcs shm

------ Shared Memory Segments --------
key        shmid      owner      perms      bytes      nattch     status      
0x52020679 2097153    adobe   666        93608      8                       

------ Semaphore Arrays --------
key        semid      owner      perms      nsems     
0x52020678 4227081    adobe   666        1         

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages    

adobe@selma:~$ ipcrm shm 2097153                             
1 resource(s) deleted
adobe@selma:~$ systemctl start nlserver
adobe@selma:~$ systemctl start apache2
```

>[!NOTE]
>
>Linux の場合、 **webTrackingParamSize** または **maxSharedLogs** パラメーターを使用する場合、共有メモリ (SHM) のサイズを増やす必要が生じる場合があります。
