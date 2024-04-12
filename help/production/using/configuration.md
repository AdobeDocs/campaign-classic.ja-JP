---
product: campaign
title: 追加の設定
description: 設定
feature: Monitoring, Configuration
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
exl-id: 80d388fd-873c-4a08-b8b6-697988f2a18c
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 26%

---

# 設定{#configuration}



## syslogd リスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、 **syslogd** リスニング ポートは 666 （udp）です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaign モジュールで考慮されます。

### Linux の場合 {#in-linux}

を編集する **customer.sh** ファイルを開き、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windows の場合 {#in-windows}

を作成する必要があります **TRACE_ADDR** を使用した環境変数 **localhost** 値： **`<listening port="" />`**.

>[!IMPORTANT]
>
>この環境変数を作成した後、プラットフォームが機能していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。テクニカルゾーンの設定は、Adobe Campaign サーバーの設定ファイルで実行されます。 オペレーターのセキュリティゾーンへのリンクは、コンソール（ **[!UICONTROL 管理/ アクセス管理/ オペレーター]** ノード）に含まれます。

>[!NOTE]
>
>セキュリティゾーンの設定について詳しくは、次を参照してください。 [この節](../../installation/using/security-zones.md).
