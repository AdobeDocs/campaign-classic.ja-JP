---
solution: Campaign Classic
product: campaign
title: 接続のしきい値
description: 接続のしきい値
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 50f95d7156e7104d90fa7a31eea30711b9c11bbf
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---


# 接続のしきい値{#connection-thresholds}

負荷の高いサーバーでは、接続のしきい値を超える可能性があります。 どのイベントでも、理由を知るのが役に立ちます。

しきい値は次の3種類です。

* **Web接続のしきい値**。Webサーバーで設定します。 変更する場合は、システム管理者に問い合わせてください。

* **データベース接続のしきい値**。 変更する場合は、データベース管理者に問い合わせてください。

* **Adobe Campaign接続のしきい値**&#x200B;は、次の2か所で入手できます。

   * **** トムカットサイド：adobe campaignTomcatクライアントに実際に到着するすべてのクエリ。

      このしきい値は、**nl6/tomcat-8/conf/server.xml**&#x200B;ファイルで設定します。 **maxThreads**&#x200B;属性を使用すると、一度に処理されるクエリ数のしきい値を増やすことができます。 例えば250に変更できます。

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

   * **データベース**:プロセスによってデータベース上で同時に開かれるすべての接続のセット。

      このしきい値は、ファイル&#x200B;**nl6/conf/serverConf.xml**&#x200B;で設定します。 **datasource pool**&#x200B;にある&#x200B;**maxCnx**&#x200B;属性を使用すると、同時に処理されるクエリのしきい値を増やすことができます。

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

