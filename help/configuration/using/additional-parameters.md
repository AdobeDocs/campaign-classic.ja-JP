---
product: campaign
title: 追加の web トラッキングパラメーター
description: Web トラッキングのパラメーターの詳細情報
feature: Configuration, Instance Settings
role: Data Engineer, Developer
exl-id: d14d94fd-b078-4893-be84-31d37a1d50f5
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 追加の web トラッキングパラメーター{#additional-parameters}

## パラメーターの定義 {#definition-of-parameters}

Adobe Campaign プラットフォームには、標準として 2 つの TRANSACTION タイプの web トラッキングパラメーターが用意されています。

* **量**：トランザクションの量を表し、
* **記事**：トランザクションの項目数を表します。

これらのパラメーターは、 **nms:webTrackingLog** レポートに表示される指標の一部を示します。

追加パラメーターを定義するには、このスキーマを拡張する必要があります。

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

サーバー設定では、web トラッキングパラメーターに考慮する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮する最大文字数を増やすと、プラットフォームの web トラッキングパフォーマンスに影響を与える可能性があります。

これを行うには、 **webTrackingParamSize** 属性 **`<trackinglogd>`** 内の要素 **serverConf.xml** ファイル。 このファイルは **conf** Adobe Campaign インストールディレクトリのサブディレクトリ。

**例**：

デフォルト値は 64 文字です。 この値を使用すると、 **量** および **記事** （&quot;amount=xxxxxxxx&amp;article=xxxxxxxx&quot;）標準パラメーター。

上記の拡張スキーマの例で示した両方のパラメーター（名前のサイズ +値のサイズ）を考慮すると、100 文字を考慮するように設定を変更できます（「amount=xxxxxxxxx&amp;article=xxxxxxxx&amp;mode=xxxxxxxxxx&amp;code=xxxxx」）。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定を変更した場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストする web サーバーを停止します（Apache、IIS など）。
* Adobe Campaign サーバーを停止します。 **net stop nlserver6** windows の場合、 **/etc/init.d/nlserver6 停止** linux の場合

  >[!NOTE]
  >
  >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl stop nlserver**

* Linux では、を使用して共有メモリセグメントを削除します。 **ipcrm** コマンド、
* Adobe Campaign サーバーを再起動します。 **net start nlserver6** windows の場合、 **/etc/init.d/nlserver6 開始** linux の場合

  >[!NOTE]
  >
  >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver**

* Web サーバーを再起動します。

**例**:Linux での設定を考慮

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
>Linux の場合、のサイズを大きくすると **webTrackingParamSize** または **maxSharedLogs** パラメータを使用する場合は、共有メモリ（SHM）のサイズを大きくする必要があります。
