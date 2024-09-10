---
product: campaign
title: 追加の設定
description: 設定
feature: Monitoring, Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
exl-id: 80d388fd-873c-4a08-b8b6-697988f2a18c
source-git-commit: 7906e9fee164d731659bbb9f96394faca5961240
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 27%

---

# 設定{#configuration}



## syslogd リスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、**syslogd** リスニングポートは 666 （udp）です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaign モジュールで考慮されます。

### Linux の場合 {#in-linux}

**customer.sh** ファイルを編集して、次の行を追加します。

```sql
export TRACE_ADDR=localhost:<listening port>
```

### Windows の場合 {#in-windows}

**localhost** の値を持つ **environment_ADDR** TRACE変数を作成する必要があります：**`<listening port="" />`**。

>[!IMPORTANT]
>
>この環境変数を作成した後、プラットフォームが機能していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。テクニカルゾーンの設定は、Adobe Campaign サーバーの設定ファイルで実行されます。 オペレーターとセキュリティゾーンのリンクは、コンソール（**[!UICONTROL 管理/アクセス管理/オペレーター]** ノード）で定義する必要があります。

>[!NOTE]
>
>セキュリティゾーンの設定については、[ この節 ](../../installation/using/security-zones.md) を参照してください。
