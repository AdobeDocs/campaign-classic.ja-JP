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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 779d9162b7296339a796512838612ede1186ddcc

---


# 設定{#configuration}

## syslogdリスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、 **syslogdリスニング** ・ポートは666(udp)です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaignモジュールで考慮されます。

### Linuxの場合 {#in-linux}

customer.sh **ファイルを編集し** 、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windowsの場合 {#in-windows}

環境変数 **TRACE_ADDR** 、 **localhostの値を使用して作成する必要があります** 。 **`<listening port="" />`**.

>[!CAUTION]
>
>この環境変数を作成した後で、お使いのプラットフォームが動作していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各演算子をゾーンにリンクする必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットに、演算子IPを含める必要があります。 技術的なゾーンの設定は、Adobe Campaignサーバーの設定ファイルで行います。 操作子のセキュリティゾーンへのリンクは、コンソール（ノード）で定義する必要が **[!UICONTROL Administration > Access management > Operators]** あります。

>[!NOTE]
>
>For more on configuring security zones, refer to [this section](../../installation/using/configuring-campaign-server.md#defining-security-zones).

