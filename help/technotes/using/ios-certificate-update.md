---
product: campaign
title: テクニカルノート - Apple プッシュ通知サービスのサーバー証明書の更新
description: Apple プッシュ通知サービスのサーバー証明書の更新
feature: Technote, Push
exl-id: 263fb4b5-ca62-4b92-a82d-8820ee998296
source-git-commit: 0143e0d6ebcdbd96d183ddd0c7f07beb149a9670
workflow-type: ht
source-wordcount: '143'
ht-degree: 100%

---

# Apple プッシュ通知サービスのサーバー証明書の更新 {#apns-certificate-update}



2024年10月17日（PT）、Apple プッシュ通知サービス（APNs）インフラストラクチャのアップデートにより Adobe Campaign Classic iOS チャネルに影響が生じました。iOS のプッシュチャネルの停止を回避するには、OS 設定の変更が&#x200B;**必須**&#x200B;です。

APNs の変更について詳しくは、[このページ](https://developer.apple.com/news/?id=09za8wzy)を参照してください。

ホステッド環境のお客様は、アクションは必要ありません。お使いの環境に新しいルート証明書が既に組み込まれています。

オンプレミス／ハイブリッド環境のお客様は、シームレスな移行を確実に実施するために、**2025年2月24日（PT）まで**&#x200B;に設定を更新する必要があります。

新しい証明書を組み込むには、次の手順に従います。

1. **SHA-2 Root : USERTrust RSA Certification Authority certificate** ルート証明書を[このページ](https://www.sectigo.com/knowledge-base/detail/Sectigo-Intermediate-Certificates/kA01N000000rfBO)からダウンロードします。

1. AAA 証明書が OS と Java の両方のトラストストアに存在することを確認します。 存在しない場合は追加します。

1. Adobe Campaign Web サービスの再起動：

   ```
   nlserver restart web
   ```
