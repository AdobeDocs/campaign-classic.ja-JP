---
product: campaign
title: テクニカルノート - Apple プッシュ通知サービスのサーバー証明書の更新
description: Apple プッシュ通知サービスのサーバー証明書の更新
feature: Technote, Push
exl-id: 263fb4b5-ca62-4b92-a82d-8820ee998296
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: ht
source-wordcount: '141'
ht-degree: 100%

---

# Apple プッシュ通知サービスのサーバー証明書の更新 {#apns-certificate-update}



2021年3月29日、Apple Push Notification サービス（APNs）インフラストラクチャのアップデートにより Adobe Campaign Classic iOS チャネルに影響が生じました。iOS のプッシュチャネルの停止を回避するには、OS 設定の変更が&#x200B;**必須**&#x200B;です。

APNs の変更について詳しくは、[このページ](https://developer.apple.com/news/?id=7gx0a2lp)を参照してください。

ホステッド環境のお客様は、アクションは必要ありません。お使いの環境に新しいルート証明書が既に組み込まれています。

オンプレミス／ハイブリッド環境のお客様は、シームレスな移行を確実に実施するために、**2021 年 3 月 29 日まで**&#x200B;に設定を更新する必要があります。

新しい証明書を組み込むには、次の手順に従います。

1. **AAACertificateServices 5/12/2020** ルート証明書を[このページ](https://support.sectigo.com/Com_KnowledgeDetailPage?Id=kA03l00000117cL)からダウンロードします。

1. AAA 証明書が OS と Java の両方のトラストストアに存在することを確認します。 存在しない場合は追加します。

1. Adobe Campaign Web サービスの再起動：

   ```
   nlserver restart web
   ```
