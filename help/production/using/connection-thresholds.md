---
title: 接続のしきい値
seo-title: 接続のしきい値
description: 接続のしきい値
seo-description: null
page-status-flag: never-activated
uuid: a4b6959a-0f5b-41a2-b4c3-d7d6613d1a18
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: f3db77db-94cc-4d75-a59b-2dddce776759
translation-type: tm+mt
source-git-commit: d509dc584cd4ae17c6dda85c09fceee8c6162dba
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 5%

---


# 接続のしきい値{#connection-thresholds}

負荷の高いサーバーでは、接続のしきい値を超える可能性があります。 どのイベントでも、理由を知るのが役に立ちます。

しきい値は次の3種類です。

1. Web接続のしきい値。Webサーバーで設定します。 変更する場合は、システム管理者に問い合わせてください。
1. データベース接続のしきい値。 変更する場合は、データベース管理者に問い合わせてください。
1. Adobe Campaign接続のしきい値は、次の2か所で指定できます。

   * Tomcat側：adobe campaignTomcatクライアントに実際に到着するすべてのクエリ。

      このしきい値は、nl6/tomcat-8/conf/server.xml **ファイルで設定します** 。 maxThreads **** 属性を使用すると、一度に処理されるクエリ数のしきい値を増やすことができます。 例えば250に変更できます。

      ```
      <Connector protocol="HTTP/1.1" port="8080"
                     maxThreads="75"
                     minSpareThreads="5"
                     enableLookups="true" redirectPort="8443"
                     acceptCount="100" connectionTimeout="20000"
                     disableUploadTimeout="true" />
          <Engine name="Tomcat-Standalone" defaultHost="localhost">
            <Host name="localhost" appBase="./"
                  unpackWARs="true" autoDeploy="true">
      ```

   * データベース：プロセスによってデータベース上で同時に開かれるすべての接続のセット。

      このしきい値は、ファイルnl6/conf/serverConf.xmlで設定し **ます**。 デー **タソースプールにある** maxCnx **** 属性を使用すると、同時に処理されるクエリのしきい値を増やすことができます。

      ```
          <!-- Data source
               -->
            <dataSource name="default">
              <dbcnx NChar="" bulkCopyUtility="" dbSchema="" encrypted="" login="" password="" provider="" server="" timezone="" unicodeData="" useTimestampTZ=""/>
              <sqlParams funcPrefix="">
                <postConnectSQL/>
              </sqlParams>
              <pool aliveTestDelaySec="600" freeCnx="0" maxCnx="90" maxIdleDelaySec="1200"/>
            </dataSource>
      ```

