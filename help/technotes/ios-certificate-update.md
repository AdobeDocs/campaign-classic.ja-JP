---
solution: Campaign Classic
product: campaign
title: テクノテ
description: テクノテ
hide: false
hidefromtoc: true
translation-type: tm+mt
source-git-commit: a21f970b6b81105517a11bcbd7f334173acc76e4
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Apple Push Notificationサービスサーバー証明書の更新{#apns-certificate-update}

2021年3月29日に、Apple Push Notification Service(APNs)インフラストラクチャの更新がAdobe Campaign ClassiciOSのチャネルに影響を与えます。 iOSのプッシュチャネルの停止を回避するため、OSの構成は&#x200B;**必須**&#x200B;に変更されました。

APNsの変更に関する詳細は、このページ[を参照してください。](https://developer.apple.com/news/?id=7gx0a2lp)

ホストされるお客様は、次の操作は必要ありません。Adobeは既に新しいルート証明書を環境に組み込んでいます。

オンプレミス/ハイブリッドのお客様は、2021年3月29日&#x200B;**までにシームレスなトランジション**&#x200B;を確実に行えるように、設定を更新する必要があります。

新しい証明書を組み込むには、次の手順に従います。

1. **AAACertificateServices 5/12/2020**&#x200B;ルート証明書[をこのページ](https://support.sectigo.com/Com_KnowledgeDetailPage?Id=kA03l00000117cL)からダウンロードします。

1. OS Trust Store追加に送信します。

1. Adobe CampaignWebサービスの再起動：

   ```
   nlserver restart web
   ```
