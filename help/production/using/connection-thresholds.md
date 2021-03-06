---
product: campaign
title: 接続のしきい値
description: 接続のしきい値
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 4ee05559-e719-4e6e-b42c-1e82df428871
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---

# 接続のしきい値{#connection-thresholds}

![](../../assets/v7-only.svg)

負荷の高いサーバーでは、接続しきい値を超える場合があります。 どのような場合でも、理由を調べるのに役立ちます。

次の 3 つのしきい値があります。

* この **Web 接続しきい値**（Web サーバーで設定） 変更するには、システム管理者に問い合わせてください。

* この **データベース接続しきい値**. 変更するには、データベース管理者に問い合わせてください。

* この **Adobe Campaign接続しきい値**（2 か所で利用可能）

   * **Tomcat** サイド：実際にAdobe Campaign Tomcat クライアントに到達するすべてのクエリ。

      このしきい値は、 **nl6/tomcat-8/conf/server.xml** ファイル。 この **maxThreads** 属性を使用すると、一度に処理されるクエリ数のしきい値を増やすことができます。 例えば、250 に変更できます。

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

      このしきい値はファイルで設定されています **nl6/conf/serverConf.xml**. この **maxCnx** 属性 **データソースプール** を使用すると、同時に処理されるクエリのしきい値を増やすことができます。

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
