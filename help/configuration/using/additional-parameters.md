---
title: その他のWebトラッキングパラメーター
description: Webトラッキングのパラメーターの詳細
page-status-flag: never-activated
uuid: c223c84a-f8fd-43d3-9deb-b1c19d442c65
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 1b2ae224-8406-4506-b589-6e5f6631e87f
translation-type: tm+mt
source-git-commit: 36fef519be93b33d55a96992c1ce234f2eaea696
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---


# 追加のパラメーター{#additional-parameters}

## パラメーターの定義 {#definition-of-parameters}

Adobe Campaignプラットフォームでは、標準として2つのTRANSACTION型Webトラッキングパラメーターをオファーします。

* **amount**:は、トランザクションの金額を表します。
* **記事**:トランザクション内の項目数を表します。

これらのパラメーターは **nms:webTrackingLog** スキーマで定義され、レポートに表示されるインジケーターの一部です。

追加のパラメーターを定義するには、このスキーマーを拡張する必要があります。

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

(配信ーまたは受信者ーの)トラッキングログリストを設定することで、これらのパラメーターの値を表示できます。

## リダイレクトサーバーの構成 {#redirection-server-configuration}

サーバー設定では、Webトラッキングパラメーターに対して考慮する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮に入れる最大文字数を増やすと、プラットフォームのWebトラッキングのパフォーマンスに影響を与える可能性があります。

これを行うには、 **serverConf.xml** ファイルの **`<trackinglogd>`****** 要素のwebTrackingParamSize属性を変更します。 このファイルは、Adobe Campaignのインストールディレクトリの **conf** サブディレクトリに保存されます。

**例**：

デフォルト値は64文字です。 この値を使用すると、 **amount** と **article** (&quot;amount=xxxxxxx&amp;article=xxxxxxxxxx&quot;)の標準パラメーターを考慮に入れることができます。

上記の拡張スキーマの例に示した両方のパラメーター（名前のサイズと値のサイズ）を考慮し、設定を変更して100文字を考慮に入れることができます(&quot;amount=xxxxxxxx&amp;article=xxxxxxxx&amp;mode=xxxxxxxx&amp;code=xxxxxx&quot;)。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストするWebサーバー（Apache、IISなど）を停止し、
* Adobe Campaignサーバーを停止します。 **net stop nlserver6** (Windows)、 **/etc/init.d/nlserver6 stop** in Linux、

   >[!NOTE]
   >
   >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。 **systemctl stop nlserver**

* Linuxでは、 **ipcrm** コマンドを使用して共有メモリセグメントを削除します。
* Adobe Campaignサーバーを再起動します。 **Windowsでのnet開始nlserver6** 、 **Linuxでの** /etc/init.d/nlserver6開始、

   >[!NOTE]
   >
   >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。 **systemctl開始nlserver**

* Webサーバーを再起動します。

**例**:Linuxの設定を考慮に入れて。

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
>Linuxでは、 **webTrackingParamSize** またはmaxSharedLogs **** パラメーターのサイズを増やすと、共有メモリ(SHM)のサイズを増やす必要がある場合があります。

