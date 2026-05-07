---
product: campaign
title: その他の設定
description: 設定
feature: Monitoring, Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
exl-id: 80d388fd-873c-4a08-b8b6-697988f2a18c
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 35%

---

# 設定{#configuration}



## syslogd リスニングポートの変更 {#changing-the-syslogd-listening-port}

デフォルトでは、**syslogd** リスニングポートは666 （udp）です。 必要に応じて、環境変数を使用して変更できます。

設定が完了すると、この変数はすべてのAdobe Campaign モジュールで考慮されます。

### Linuxでは {#in-linux}

**customer.sh** ファイルを編集し、次の行を追加します。

```sql
export TRACE_ADDR=localhost:<listening port>
```

### Windowsの場合 {#in-windows}

**TRACE_ADDR**&#x200B;環境変数を&#x200B;**localhost**&#x200B;値&#x200B;**`<listening port="" />`**&#x200B;で作成する必要があります。

>[!IMPORTANT]
>
>この環境変数を作成した後、プラットフォームが機能していることを確認するために、いくつかのテストを実行することをお勧めします。

## セキュリティゾーンの設定 {#configuring-security-zones}

インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。 テクニカルゾーンの設定は、Adobe Campaign サーバーの設定ファイルで行います。 オペレーターのセキュリティゾーンへのリンクは、コンソールで定義する必要があります（**[!UICONTROL 管理/ アクセス管理/ オペレーター]** ノード）。

>[!NOTE]
>
>セキュリティゾーンの設定について詳しくは、[この節](../../installation/using/security-zones.md)を参照してください。
