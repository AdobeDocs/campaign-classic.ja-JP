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
feature_v2: []
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 19%

---

# 接続のしきい値{#connection-thresholds}



負荷の大きいサーバーの場合、接続しきい値を超える可能性があります。 いずれにせよ、その理由を知ることは便利です。

3つの異なるしきい値があります。

* Web サーバーで構成されている&#x200B;**Web接続しきい値**。 変更するには、システム管理者にお問い合わせください。

* **データベース接続しきい値**。 変更するには、データベース管理者にお問い合わせください。

* **Adobe Campaign接続しきい値**&#x200B;は、次の2つの場所で利用できます。

   * **Tomcat**&#x200B;側：すべてのクエリが実際にAdobe Campaign Tomcat クライアントに届きます。

     このしきい値は、**nl6/tomcat-X/conf/server.xml** ファイルで設定されています。 **maxThreads**&#x200B;属性を使用すると、一度に処理されるクエリの数のしきい値を増やすことができます。 例えば、250に変更できます。

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

   * **データベース**: プロセスによってデータベース上で同時に開かれるすべての接続のセット。

     このしきい値はファイル **nl6/conf/serverConf.xml**&#x200B;で設定されています。 **データソースプール**&#x200B;にある&#x200B;**maxCnx**&#x200B;属性を使用すると、同時に処理されるクエリのしきい値を増やすことができます。

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
