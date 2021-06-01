---
product: campaign
title: 設定
description: 設定
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 80d388fd-873c-4a08-b8b6-697988f2a18c
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 3%

---

# 設定{#configuration}

## syslogdリスニングポート{#changing-the-syslogd-listening-port}の変更

デフォルトでは、**syslogd**&#x200B;リスニングポートは666(udp)です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaignモジュールで考慮されます。

### Linuxの場合{#in-linux}

**customer.sh**&#x200B;ファイルを編集し、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windowsの場合{#in-windows}

**localhost**&#x200B;値を使用して&#x200B;**TRACE_ADDR**&#x200B;環境変数を作成する必要があります。**`<listening port="" />`**&#x200B;と入力します。

>[!IMPORTANT]
>
>この環境変数を作成した後で、プラットフォームが機能していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各オペレーターをゾーンにリンクする必要があります。また、セキュリティゾーンに定義されているアドレスまたはアドレスセットにオペレーターのIPを含める必要があります。 テクニカルゾーンの設定は、Adobe Campaignサーバーの設定ファイルで実行されます。 オペレーターとセキュリティゾーンのリンクは、コンソール（ **[!UICONTROL 管理/アクセス管理/オペレーター]**&#x200B;ノード）で定義する必要があります。

>[!NOTE]
>
>セキュリティゾーンの設定について詳しくは、[この節](../../installation/using/security-zones.md)を参照してください。
