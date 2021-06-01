---
product: campaign
title: 追加のWebトラッキングパラメーター
description: Webトラッキングのパラメーターの詳細を説明します
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: d14d94fd-b078-4893-be84-31d37a1d50f5
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---

# 追加パラメーター{#additional-parameters}

## パラメータの定義{#definition-of-parameters}

Adobe Campaignプラットフォームでは、2つのトランザクションタイプWebトラッキングパラメーターが標準として提供されています。

* **量**:トランザクションの金額を表します。
* **記事**:トランザクション内の品目数を表します。

これらのパラメーターは&#x200B;**nms:webTrackingLog**&#x200B;スキーマで定義され、レポートに表示される指標の一部です。

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

## リダイレクションサーバーの構成{#redirection-server-configuration}

サーバーの設定で、Webトラッキングパラメーターに使用する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮する最大文字数を増やすと、プラットフォームのWebトラッキングパフォーマンスに影響を与える可能性があります。

これをおこなうには、**serverConf.xml**&#x200B;ファイルの&#x200B;**`<trackinglogd>`**&#x200B;要素の&#x200B;**webTrackingParamSize**&#x200B;属性を変更します。 このファイルは、Adobe Campaignインストールディレクトリの&#x200B;**conf**&#x200B;サブディレクトリに保存されます。

**例**：

デフォルト値は64文字です。 この値を使用すると、**amount**&#x200B;および&#x200B;**article**(&quot;amount=xxxxxxx&amp;article=xxxxxxxx&quot;)標準パラメーターを考慮に入れることができます。

上記の拡張スキーマの例で示した両方のパラメーター（名前のサイズ+値のサイズ）を考慮することで、100文字を考慮に入れるように設定を変更できます(「amount=xxxxxxxxx&amp;article=xxxxxxx&amp;mode=xxxxxxxxxxxxxxxx&amp;code=xxx」)。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストするWebサーバー（Apache、IISなど）を停止します。
* Adobe Campaignサーバーを停止します。**Windowsでは** net stop nlserver6 **、Linuxでは/etc/init.d/nlserver6 stop**

   >[!NOTE]
   >
   >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。**systemctl stop nlserver**

* Linuxでは、**ipcrm**&#x200B;コマンドを使用して共有メモリセグメントを削除します。
* Adobe Campaignサーバーを再起動します。**Windowsでは**/etc/init.d/nlserver6 start **、Linuxではnet start nlserver6**

   >[!NOTE]
   >
   >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。**systemctl start nlserver**

* Webサーバーを再起動します。

**例**:Linuxでの設定を考慮して

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
>Linuxの場合、**webTrackingParamSize**&#x200B;または&#x200B;**maxSharedLogs**&#x200B;パラメーターのサイズを大きくすると、共有メモリ(SHM)のサイズを大きくする必要が出る場合があります。
