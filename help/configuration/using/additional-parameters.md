---
title: その他のパラメーター
seo-title: その他のパラメーター
description: その他のパラメーター
seo-description: null
page-status-flag: never-activated
uuid: c223c84a-f8fd-43d3-9deb-b1c19d442c65
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 1b2ae224-8406-4506-b589-6e5f6631e87f
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 912507f25c5bc3c1ca7121b0df8182176900f4c0

---


# Additional parameters{#additional-parameters}

## パラメーターの定義 {#definition-of-parameters}

Adobe Campaignプラットフォームでは、標準として2つのTRANSACTIONタイプのWebトラッキングパラメーターを提供しています。

* **金額**:は、取引の金額を表します。
* **記事**:トランザクション内の項目数を表します。

これらのパラメーターは **nms:webTrackingLogスキーマで定義され** 、レポートに表示されるインジケーターの一部です。

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

## リダイレクトサーバーの構成 {#redirection-server-configuration}

サーバー設定では、Webトラッキングパラメーターに考慮する最大文字数を定義できます。

>[!CAUTION]
>
>考慮に入れる最大文字数を増やすと、プラットフォームのWebトラッキングのパフォーマンスに影響を与える可能性があります。

これを行うには、 **serverConf.xmlファイル内の要素** のwebTrackingParamSize属性を **`<trackinglogd>`** 変更します **** 。 このファイルは、Adobe Campaignインストールディレクトリの **conf** サブディレクトリに保存されます。

**例**：

デフォルト値は64文字です。 この値を使用すると、amountと **article****** (「amount=xxxxxxxx&amp;article=xxxxxxxxxxx」)の標準パラメーターを考慮できます。

上記の拡張スキーマの例で示した両方のパラメーター（名前のサイズと値のサイズ）を考慮して、100文字を考慮するように設定を変更できます(「amount=xxxxxxxxxx&amp;article=xxxxxxxxx&amp;mode=xxxxxxxxxxx&amp;code=xxxxxx」)。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストするWebサーバー（Apache、IISなど）を停止し、
* Adobe Campaignサーバーを停止します。 **net stop nlserver6** (Windows)、 **/etc/init.d/nlserver6 stop** (Linux)、
* Linuxでは、 **ipcrmコマンドを使用して共有メモリセグメントを削除します** 。
* Adobe Campaignサーバーを再起動します。Windowsで **は** net start nlserver6 **、** Linuxでは/etc/init.d/nlserver6 start、
* Webサーバーを再起動します。

**例**:Linuxの設定を考慮に入れて

```
adobe@selma:~$ /etc/init.d/nlserver6 stop
adobe@selma:~$ /etc/init.d/apache stop
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
adobe@selma:~$ /etc/init.d/nlserver6 start
adobe@selma:~$ /etc/init.d/apache start
```

>[!NOTE]
>
>Linuxでは、webTrackingParamSizeまたは **maxSharedLogs** パラメーターのサイズを増やすと **** 、共有メモリ(SHM)のサイズを増やす必要が生じる場合があります。

