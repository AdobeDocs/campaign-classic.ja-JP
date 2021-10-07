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

Adobe Campaignプラットフォームでは、標準として 2 つのトランザクションタイプの Web トラッキングパラメーターが用意されています。

* **量**:トランザクションの金額を表します。
* **記事**:トランザクション内の品目数を表します。

これらのパラメーターは **nms:webTrackingLog** スキーマで定義され、レポートに表示される指標の一部です。

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

（配信または受信者の）トラッキングログリストを設定して、これらのパラメーターの値を表示できます。

## リダイレクトサーバーの構成 {#redirection-server-configuration}

サーバーの設定で、Web トラッキングパラメーターに使用する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮する最大文字数を増やすと、プラットフォームの Web トラッキングのパフォーマンスに影響を与える可能性があります。

そのためには、**serverConf.xml** ファイルの **`<trackinglogd>`** 要素の **webTrackingParamSize** 属性を変更します。 このファイルは、Adobe Campaignインストールディレクトリの **conf** サブディレクトリに保存されます。

**例**：

デフォルト値は 64 文字です。 この値を使用すると、**amount** および **article**(&quot;amount=xxxxxxx&amp;article=xxxxxxx&quot;) 標準パラメーターを考慮に入れることができます。

上記の拡張スキーマの例で示した両方のパラメーター（名前のサイズと値のサイズ）を考慮することで、100 文字を考慮に入れるように設定を変更できます (&quot;amount=xxxxxxxx&amp;article=xxxxxxxx&amp;mode=xxxxxxxxxxx&amp;code=xxxxx&quot;)。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストする Web サーバー（Apache、IIS など）を停止します。
* Adobe Campaignサーバーを停止します。**Windows では** net stop nlserver6 **、Linux では /etc/init.d/nlserver6 stop**

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl stop nlserver**

* Linux では、**ipcrm** コマンドを使用して共有メモリセグメントを削除します。
* Adobe Campaignサーバーを再起動します。**Windows では**/etc/init.d/nlserver6 start **、Linux では net start nlserver6**

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver**

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
>Linux では、**webTrackingParamSize** または **maxSharedLogs** パラメーターのサイズを大きくすると、共有メモリ (SHM) のサイズを大きくする必要が生じる場合があります。
