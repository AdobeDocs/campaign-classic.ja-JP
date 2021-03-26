---
solution: Campaign Classic
product: campaign
title: テクニカルノート
description: テクニカルノート
hide: false
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 08c6e84e07da2811c91aa58ddf40c5781de2b163
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 60%

---


# Apple Push Notificationサービスサーバー証明書の更新{#apns-certificate-update}

2021 年 3 月 29 日、Apple Push Notification Service（APN）インフラストラクチャのアップデートが Adobe Campaign Classic iOS チャネルに影響を与えます。iOS のプッシュチャネルの停止を回避するには、OS 設定の変更が&#x200B;**必須**&#x200B;です。

APNs 変更の詳細については、 [こちらのページ](https://developer.apple.com/news/?id=7gx0a2lp)を参照してください。

アクションは必要ありません。アドビはすでに新しいルート証明書を環境に組み込んでいます。

オンプレミス／ハイブリッドのお客様は、シームレスにトランジションできるよう、**2021 年 3 月 29 日までに**&#x200B;設定を更新する必要があります。

新しい証明書を組み込むには、次の手順に従います。

1. **AAACertificateServices 5/12/2020**&#x200B;ルート証明書[をこのページ](https://support.sectigo.com/Com_KnowledgeDetailPage?Id=kA03l00000117cL)からダウンロードします。

1. AAA証明書がOSとJAVAの両方のTrustoreに存在することを確認します。 ない場合は追加します。

1. Adobe CampaignWebサービスの再起動：

   ```
   nlserver restart web
   ```

