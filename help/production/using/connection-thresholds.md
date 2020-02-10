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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 接続のしきい値{#connection-thresholds}

負荷の高いサーバーの場合は、接続しきい値を超える可能性があります。 どのような場合でも、理由を知ると役に立ちます。

しきい値は3種類あります。

1. Webサーバーで設定されるWeb接続のしきい値。 変更するには、システム管理者に問い合わせてください。
1. データベース接続のしきい値。 変更する場合は、データベース管理者に問い合わせてください。
1. Adobe Campaignの接続しきい値は、次の2か所で使用できます。

   * Tomcat側：実際にAdobe Campaign Tomcatクライアントに到着するすべてのクエリー。

      このしきい値は、nl6/tomcat-7/conf/server.xmlファイルで **設定します** 。 maxThreads **属性を使用すると** 、一度に処理されるクエリーの数のしきい値を増やすことができます。 例えば、250に変更できます。

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

      このしきい値は、ファイルnl6/conf/serverConf.xmlで設定 **します**。 データソース **プールにある** maxCnx **属性を使用すると** 、同時に処理されるクエリーのしきい値を増やすことができます。

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

