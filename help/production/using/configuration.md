---
solution: Campaign Classic
product: campaign
title: 設定
description: 設定
audience: production
content-type: reference
topic-tags: production-procedures
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 3%

---


# 設定{#configuration}

## syslogdリスニングポートの変更{#changing-the-syslogd-listening-port}

デフォルトでは、**syslogd**&#x200B;リスニングポートは666(udp)です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaignモジュールで考慮されます。

### Linuxの場合{#in-linux}

**customer.sh**&#x200B;ファイルを編集し、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windowsの場合{#in-windows}

**localhost**&#x200B;値を使用して&lt;a0/>TRACE_ADDR **環境変数を作成する必要があります。**`<listening port="" />`**。**

>[!IMPORTANT]
>
>この環境変数を作成した後で、お使いのプラットフォームが動作していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

各オペレーターは、インスタンスにログオンするためにゾーンにリンクされている必要があります。また、セキュリティゾーンに定義されているアドレスまたはアドレスセットに、オペレーターIPを含める必要があります。 技術的なゾーンの設定は、Adobe Campaignサーバーの設定ファイルで行われます。 操作子のセキュリティゾーンへのリンクは、コンソールで定義する必要があります（**[!UICONTROL 管理/アクセス管理/操作子]**&#x200B;ノード）。

>[!NOTE]
>
>セキュリティゾーンの設定について詳しくは、[この](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。
