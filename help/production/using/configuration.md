---
product: campaign
title: 追加の設定
description: 設定
feature: Monitoring, Configuration
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
exl-id: 80d388fd-873c-4a08-b8b6-697988f2a18c
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 29%

---

# 設定{#configuration}



## syslogd リスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、 **syslogd** リスニングポートは 666(udp) です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaignモジュールで考慮されます。

### Linux の場合 {#in-linux}

を編集します。 **customer.sh** ファイルを開き、次の行を追加します。

```
export TRACE_ADDR=localhost:<listening port>
```

### Windows の場合 {#in-windows}

次を作成する必要があります： **TRACE_ADDR** 環境変数に **localhost** 値： **`<listening port="" />`**.

>[!IMPORTANT]
>
>この環境変数を作成した後で、プラットフォームが機能していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。テクニカルゾーンの設定は、Adobe Campaignサーバーの設定ファイルで実行されます。 オペレーターとセキュリティゾーンのリンクは、コンソールで定義する必要があります ( **[!UICONTROL 管理/アクセス管理/オペレーター]** ノード ) で使用できます。

>[!NOTE]
>
>セキュリティゾーンの設定について詳しくは、 [この節](../../installation/using/security-zones.md).
