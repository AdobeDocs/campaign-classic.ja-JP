---
title: 設定
seo-title: 設定
description: 設定
seo-description: null
page-status-flag: never-activated
uuid: 4316d4b2-0964-4e25-9e4f-f2378f044c85
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: 12f13b8d-afc3-4b55-a31b-080d31f84fc9
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 4%

---


# 設定{#configuration}

## syslogdリスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、 **syslogd** listeningポートは666(udp)です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaignモジュールで考慮されます。

### Linuxの場合 {#in-linux}

customer.sh **** ファイルを編集し、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windowsの場合 {#in-windows}

**localhost** 値を使用して **TRACE** _ADDR環境変数を作成する必要があります。 **`<listening port="" />`**.

>[!CAUTION]
>
>この環境変数を作成した後で、お使いのプラットフォームが動作していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

各オペレーターは、インスタンスにログオンするためにゾーンにリンクされている必要があります。また、セキュリティゾーンに定義されているアドレスまたはアドレスセットに、オペレーターIPを含める必要があります。 技術的なゾーンの設定は、Adobe Campaignサーバーの設定ファイルで行われます。 操作子のセキュリティゾーンへのリンクは、コンソールで定義する必要があります( **[!UICONTROL 管理/アクセス管理/操作子]** ノード)。

>[!NOTE]
>
>For more on configuring security zones, refer to [this section](../../installation/using/configuring-campaign-server.md#defining-security-zones).

