---
product: campaign
title: 追加のweb トラッキングパラメーター
description: Web トラッキングのパラメーターについて詳しく見る
feature: Configuration, Instance Settings
role: Developer
exl-id: d14d94fd-b078-4893-be84-31d37a1d50f5
TQID: https://experienceleague.adobe.com/sk3BZJWu9TH134z5a36k3VlQepW-od7ar0vEWrwTMN0
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 0%

---

# 追加のweb トラッキングパラメーター{#additional-parameters}

## パラメーターの定義 {#definition-of-parameters}

Adobe Campaignでは、2つのトランザクションタイプのweb トラッキングパラメーターを標準として提供しています。

* **amount**: トランザクションの金額を表します。
* **記事**: トランザクション内の項目数を表します。

これらのパラメーターは、**nms:webTrackingLog** スキーマで定義され、レポートに表示される指標の一部です。

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

## リダイレクションサーバー設定 {#redirection-server-configuration}

サーバー設定では、web トラッキングパラメーターに考慮する最大文字数を定義できます。

>[!IMPORTANT]
>
>考慮される最大文字数を増やすと、プラットフォームのweb トラッキングのパフォーマンスに影響を与える可能性があります。

これを行うには、**serverConf.xml** ファイルの&#x200B;**`<trackinglogd>`**&#x200B;要素の&#x200B;**webTrackingParamSize**&#x200B;属性を変更します。 このファイルは、Adobe Campaign インストールディレクトリの&#x200B;**conf** サブディレクトリに保存されます。

**例**：

デフォルト値は64文字です。 この値を使用すると、**amount**&#x200B;および&#x200B;**article** （&quot;amount=xxxxxxxx&amp;article=xxxxxxxx&quot;）標準パラメーターを考慮できます。

上記の拡張スキーマの例で示されている両方のパラメーター（名前のサイズと値のサイズ）を考慮して、設定を変更して100文字を考慮することができます（&quot;amount=xxxxxxxx&amp;article=xxxxxxxx&amp;mode=xxxxxxxxxx&amp;code=xxxxx&quot;）。

```
<trackinglogd args="" autoStart="false" initScript="" maxCreateFileRetry="5" maxLogsSizeOnDiskMb="500"
maxProcessMemoryAlertMb="1800" maxProcessMemoryWarningMb="1600" maxSharedLogs="25000"
processRestartTime="06:00:00" purgeLogsPeriod="50000" runLevel="10"
webTrackingParamSize="64"/>
```

設定が変更された場合は、次の操作を行う必要があります。

* リダイレクトモジュールをホストするweb サーバー（Apache、IISなど）を停止します。
* Windowsでは&#x200B;**net stop nlserver6**、Linuxでは&#x200B;**/etc/init.d/nlserver6 stop**&#x200B;というAdobe Campaign サーバーを停止します。

  >[!NOTE]
  >
  >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）: **systemctl stop nlserver**

* Linuxでは、**ipcrm** コマンドを使用して共有メモリセグメントを削除します。
* Windowsで&#x200B;**net start nlserver6**、Linuxで&#x200B;**/etc/init.d/nlserver6 start**&#x200B;のAdobe Campaign サーバーを再起動します。

  >[!NOTE]
  >
  >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）: **systemctl start nlserver**

* Web サーバーを再起動します。

**例**: Linuxでの設定を考慮します。

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
>Linuxの場合、**webTrackingParamSize**&#x200B;または&#x200B;**maxSharedLogs** パラメーターのサイズを増やす場合、共有メモリ （SHM）のサイズを増やす必要がある場合があります。
