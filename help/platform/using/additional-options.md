---
title: 外部データベースへのアクセス
seo-title: 外部データベースへのアクセス
description: 外部データベースへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c86af066045c1c35b51624de8565af21746354c1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 100%

---


# 追加のオプション {#additional-options}

<!--

## HTTP relay to a remote instance {#http-relay-to-a-remote-instance}

You can access external databases configured in remote instances using the HTTP protocol.

>[!NOTE]
>
>Not all SQL data types are supported by this feature. Blob data types are not supported at all. It is possible that other data types may not work depending on the targeted database (Timestamp on Microsoft SQL Server, for example). Please contact Adobe support for more information.

This simplifies transferring and synchronizing data between two instances. It also enables you to sidestep any tunneling between an instance and a remote database as well as the installation of the client layers to access this database. The destination instance can be a hosted instance.

>[!CAUTION]
>
>This option is only for facilitating data replication flows (ETL).   
>
>For example, it allows a cloud-hosted instance to have direct access to the data in an "on-premise" hosted database. However, it is not intended to allow targeting to be carried on an "on-premise" hosted database directly from the cloud.

To do this, you must configure the external accounts of the two instances so that the local instance can communicate with the remote instance using the HTTP protocol:

* Local instance: select the new **[!UICONTROL HTTP relay to a remote database]** connection type.

  In case of bulk load data transfer, also specify the buffer size. Select the compression option if you want to reduce the size of the transferred data.

  The **[!UICONTROL Data source]** must be defined with the following syntax: "nms:extAccount : `<internal_name_of_the_external_account>`"

  ![](assets/fda_over_http_1.png)

  >[!NOTE]
  >
  >We recommend that you use an HTTPS connection.

* Remote instance: in the FDA external account of the database accessed via the HTTP relay, check the Target of an **[!UICONTROL 'HTTP relay to a remote database' account option]**.

  ![](assets/fda_over_http_2.png)

The following example shows the new possible operating mode:

![](assets/schema_fda_over_http_2.png)

>[!CAUTION]
>
>The default database of the remote instance must be accessed via an external account as well.

This operating method avoids that the cleanup workflow of each instance deletes the work tables of the databases that use the instance as relay.

Thus, in the previous example, the cleanup workflow of the remote instance will not perform any action on the red FDA database as it is used by the local instance.

-->

## 一時的なスキーマの直接的な作成 {#directly-creating-temporary-schemas}

FDA 外部データベースへの複数のアクセスを管理する場合、新しいオプションを使って、外部アカウントの設定時に作業用スキーマを直接作成できます。

>[!NOTE]
>
>このオプションは PostgreSQL でのみ機能します。

![](assets/fda_work_table.png)

## 外部データを使用した E メールのパーソナライゼーションの最適化 {#optimizing-email-personalization-with-external-data}

ビルド 8740 から、配信プロパティの「**[!UICONTROL 分析]**」タブで「**[!UICONTROL ワークフローを使用してパーソナライゼーションデータを準備]**」オプションが使用できるようになりました。

このオプションを選択すると、配信の分析時に、一時テーブル内のターゲットにリンクするすべてのデータ（FDA にリンクするテーブルのデータなど）を保存するワークフローが自動的に作成、実行されます。

このオプションをオンにすることで、パーソナライゼーションのパフォーマンスを大幅に向上できます。

## ワークフローでの外部データベースからのデータの使用 {#using-data-from-an-external-database-in-a-workflow}

複数の Adobe Campaign ワークフローアクティビティで、外部データベースに格納されたデータを使用できます。

### 外部データのフィルタリング {#filtering-on-external-data}

「クエリ」アクティビティでは、外部データを追加して、定義したフィルター設定でそのデータを使用できます。

詳しくは、[クエリ](../../workflow/using/targeting-data.md#selecting-data)の節を参照してください。

### サブセットの作成 {#creating-sub-sets}

「分割」アクティビティでは、サブセットを作成できます。外部データを使用して、使用するフィルタリング条件を定義できます。

詳しくは、[分割](../../workflow/using/split.md)の節を参照してください。

### 外部データベースの読み込み {#loading-external-database}

「データの読み込み（RDBMS）」で外部データを使用できます。このアクティビティについては、[データの読み込み](../../workflow/using/data-loading--rdbms-.md)の節で説明しています。

### 情報およびリンクの追加 {#adding-information-and-links}

「エンリッチメント」アクティビティでは、ワークフローの作業用テーブルにデータを追加したり、リンクを外部テーブルに追加したりすることができます。このため、外部データベースからのデータを活用できます。この手順は、[エンリッチメント](../../workflow/using/enrichment.md)の節で説明しています。
<!--

## Cloud Messaging - FDA synchronization {#cloud-messaging---fda-synchronization}

When the Cloud Messaging server and the Marketing server have not been synchronized for a long period, the volume of missing broadlogs on the Marketing server can be significant. To optimize broadlog synchronization via the FDA, the **NmsMidSourcing_LogsPeriodHour** option has been added. This allows a maximum period (expressed in hours) to be specified as to limit the number of broadlogs recovered every time the synchronization workflow is executed.

The option is to be added in the console, in the **[!UICONTROL Administration > Options]** node.

>[!CAUTION]
>
>This option must **only** be used for synchronizing a significant volume of broadlogs via the FDA.

>[!NOTE]
>
>The option is only taken into account if a last recovery date exists (**NmsMidSourcing_LastBroadLog_&#42;** option).

## Message Center - Read access on the XtkFolder table {#message-center---read-access-on-the-xtkfolder-table}

From build 8141 and above, manual action is necessary if Message Center uses the FDA as an archiving mode.

You need to grant read access on the XtKFolder table to the user linked with the external FDA account.

For a PostgreSQL database for example, the command is as follows:

```
GRANT SELECT ON XtkFolder TO DBUSER;
```

This user must have read access to the following tables:

* NmsBroadLogRtEvent
* NmsBroadLogBatchEvent
* NmsTrackingLogRtEvent
* NmsTrackingLogBatchEvent
* NmsRtEvent
* NmsBatchEvent
* NmsBroadLogMsg
* NmsTrackingUrl
* NmsDelivery
* NmsWebTrackingLog

>[!NOTE]
>
>This modification deletes the "Permission denied for relation xtkfolder" error message.

If the working schema selected in the external FDA account is not the out-of-the-box Neolane account, then this modification to the access rights is not necessary.

-->

