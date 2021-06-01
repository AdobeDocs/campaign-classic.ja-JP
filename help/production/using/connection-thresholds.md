---
product: campaign
title: 接続のしきい値
description: 接続のしきい値
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 4ee05559-e719-4e6e-b42c-1e82df428871
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---

# 接続のしきい値{#connection-thresholds}

負荷の高いサーバーでは、接続のしきい値を超える場合があります。 どのような場合でも、理由を調べると役に立ちます。

次の3つのしきい値があります。

* Webサーバーで設定されている&#x200B;**Web接続のしきい値**。 変更するには、システム管理者に問い合わせてください。

* **データベース接続のしきい値**。 変更するには、データベース管理者に問い合わせてください。

* **Adobe Campaign接続のしきい値**&#x200B;は、次の2か所で使用できます。

   * **** トムカットサイド：実際にAdobe Campaign Tomcatクライアントに到達するすべてのクエリ。

      このしきい値は、**nl6/tomcat-8/conf/server.xml**&#x200B;ファイルで設定します。 **maxThreads**&#x200B;属性を使用すると、一度に処理されるクエリ数のしきい値を増やすことができます。 例えば、250に変更できます。

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

      このしきい値は、ファイル&#x200B;**nl6/conf/serverConf.xml**&#x200B;で設定します。 **データソースプール**&#x200B;にある&#x200B;**maxCnx**&#x200B;属性を使用すると、同時に処理されるクエリのしきい値を増やすことができます。

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
