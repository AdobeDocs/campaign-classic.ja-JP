---
product: campaign
title: 接続のしきい値
description: 接続のしきい値
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 4ee05559-e719-4e6e-b42c-1e82df428871
source-git-commit: 757e3a5395f24e0bdd04737aba0458881e4ea780
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 10%

---

# 接続のしきい値{#connection-thresholds}



負荷の高いサーバーでは、接続のしきい値を超える場合があります。 いずれにせよ、その理由を見つけることは有用です。

しきい値は次の 3 つです。

* この **Web 接続のしきい値**、web サーバーで設定されます。 変更するには、システム管理者に問い合わせてください。

* この **データベース接続のしきい値**. 変更するには、データベース管理者に問い合わせてください。

* この **Adobe Campaign接続のしきい値**、次の 2 つの場所で利用できます。

   * **Tomcat** 側：実際にAdobe Campaign Tomcat クライアントに到達するすべてのクエリ。

     このしきい値は、 **nl6/tomcat-X/conf/server.xml** ファイル。 この **maxThreads** 属性を使用すると、一度に処理するクエリ数のしきい値を増やすことができます。 例えば、250 に変更できます。

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

   * **データベース**：プロセスによってデータベースで同時に開かれたすべての接続のセット。

     このしきい値は、ファイルで設定されます **nl6/conf/serverConf.xml**. この **maxCnx** に配置された属性 **データソースプール** 同時に処理するクエリのしきい値を増やすことができます。

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
