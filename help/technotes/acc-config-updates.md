---
solution: Campaign Classic
product: campaign
title: テクノテ
description: テクノテ
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 1a7ec4899bc0fab3935c25918c586a20afb88d1a
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 10%

---


# Adobe Campaign構成の更新 — 2021年3月{#acc-config-updates}

最新のビルドおよび製品修正を使用して、インフラストラクチャと設定を更新しておく必要があります。 これらの修正は、サービスの継続性とセキュリティを確保するために必須です。

キャンペーンユーザーは、次の最新バージョンのいずれかにアップグレードする必要があります。

* ゴールドスタンダード11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース.[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース.[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース.[詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース.[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース.[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース.[詳細情報](../rn/using/release--19-1.md)

これらのビルドは、特定のキャンペーンサービスの継続性を確保します。Experience Cloudトリガー統合、APNs認証、およびAdobeIdentity Managementサービス(IMS)認証メカニズムに影響する新しい接続プロトコル。

ホストをご利用のお客様は、必要なビルドのアップグレードを定期的に行うことをAdobeからお知らせします。 コンプライアンスを確保するために、推奨事項に従ってアップグレードする必要があります。

オンプレミス/ハイブリッドのお客様は、上記のいずれかのバージョンにアップグレードする必要があります。 また、環境が安全で、Adobeやサードパーティ製システムの変更が今後行われる準備を整えるために、いくつかの手動タスクを行う必要があります。

>[!NOTE]
>
>これらの変更点に関するご質問は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## セキュリティの更新

最新のキャンペーンバージョンには、SSRF(Server Side Request Forgery)の問題に対する保護を強化するセキュリティ修正が付属しています。 詳細[は、このページ](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)を参照してください。

**影響を受けているか**

環境がキャンペーン19.1.8、19.2.4、20.1.4、20.2.4、20.3.3またはGold Standard 11よりも低いビルドの場合は、影響を受けます。

**更新方法**

上記の新しいビルドの1つにアップグレードする必要があります。

* ハイブリッド顧客の場合、Adobeはミッドソーシングインスタンスを新しいバージョンにアップグレードするので、そのマーケティングインスタンスもアップグレードすることを強くお勧めします。

   新しいビルドは、少なくともCampaign Classic17.9のリリースと互換性がありますが、セキュリティ上の差を防ぐため、Adobeではすべてのインスタンスを新しいビルドにアップグレードすることを強くお勧めします。 

* オンプレミスのお客様は、マーケティングインスタンスとミッドソーシングインスタンスを新しいビルドにアップグレードするように要求されます。

>[!CAUTION]
>
>今のところアップグレードできない場合は、**Adobeカスタマーケアチームに連絡して、インスタンス**&#x200B;に手動でセキュリティ修正を適用する必要があります。


## キャンペーンクライアントコンソールの更新

最新のゴールド標準11ビルドでは、配信の日付選択や画像管理など、クライアントコンソールの一部のコンポーネントを使用できない問題が修正されました。 コンソールのアップグレードは必須です。

[詳細情報](../rn/using/gold-standard.md)。

>[!NOTE]
>
>他のバージョン用の新しいクライアントコンソールは、近日中に利用可能になります。

## IMSを使用してキャンペーンに接続

AdobeIDサービス(IMS)は、2021年6月30日&#x200B;**から始まる古いバージョンのInternet Explorerのサポートを停止します。**[詳細情報](https://helpx.adobe.com/x-productkb/global/update-operating-system-and-browser.html)。キャンペーンクライアントコンソールが更新され、AdobeIMSとの互換性が確保されました。

**影響を受けているか**

Adobe ID](../integrations/using/about-adobe-id.md)経由でキャンペーン[に接続する場合は、AdobeIDサービス(IMS)を使用して、上記の新しいバージョンの1つにアップグレードする必要があります。 これらのリリースには、新しい接続プロトコルが付属しています。**2021年6月30日**&#x200B;以降、キャンペーンサーバーとクライアントコンソールの両方がキャンペーンに接続できるようにするには、アップグレードが必須です。

**更新方法**

ホストされるお客様は、次の操作は必要ありません。Adobeは既にインスタンスを新しいバージョンにアップグレードしています。

オンプレミス/ハイブリッドのお客様は、新しいクライアントコンソールのメリットを活かすために、新しいバージョンの1つにアップグレードする必要があります。また、2021年6月30日&#x200B;**までにシームレスなトランジションを確保する必要があります。**

すべてのインスタンスをアップグレードしたら、クライアントコンソールもこのバージョンにアップグレードする必要があります。

* [Adobeソフトウェア配布](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)にアクセスする方法を説明します。

* [キャンペーンクライアントコンソールのインストール方法を説明します](../installation/using/installing-the-client-console.md)。

## Experience Cloudトリガーとの統合

従来のoAuth認証サービスが提供終了に達しました。 元々、パイプラインにアクセスするためのoAUTH認証設定に基づくトリガー統合認証は、Adobe I/Oに移行しました。**2021年4月30日**&#x200B;に退役します。 [詳細情報](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411)。

**影響を受けているか**

環境がキャンペーン19.1.8、20.2.4、Gold Standard 11よりも低いビルドを使用している場合、oAuth認証を通じて古いバージョンのトリガー統合を使用しています。**Adobe I/O**&#x200B;に移動する必要があります。

**更新方法**

インスタンスを新しいバージョンにアップグレードしたら、すべてのお客様は、[手順に従って新しい認証モード](../integrations/using/configuring-adobe-io.md)に移行する必要があります。 これには、新しいAdobe I/Oトークンを生成し、実装で使用する必要があります。  

さらに、ハイブリッド環境の場合、パイプラインがミッドソーシングインスタンスで設定されていることを確認する必要があります。[詳細情報](../integrations/using/configuring-pipeline.md)。

[Adobe I/O に移行する方法を説明します](../integrations/using/configuring-adobe-io.md).

## HTTP/2ベースのAPNsプロバイダーAPI

Apple Push Notification Service(APNs)は、**2021年3月31日**&#x200B;以降、レガシーバイナリプロトコルをサポートしなくなります。 [詳細を表示](https://developer.apple.com/news/?id=c88acm2b)。

**影響を受けているか**

インスタンスがキャンペーン21.1より古いバージョンで実行され、レガシーAppleバイナリプロトコルを使用してプッシュ通知を送信する場合は、HTTP/2ベースのAPNsプロバイダーAPIに更新する必要があります。

**更新方法**

ホストされるお客様は、次の操作は必要ありません。Adobeは既にインスタンスをHTTP/2ベースのAPIに更新しています。

オンプレミス/ホストのお客様は、設定を更新する必要があります。 [HTTP/2への移行方法](https://helpx.adobe.com/jp/campaign/kb/migrate-to-apns-http2.html)

## APNsルート証明書の更新

2021年3月29日に、Apple Push Notification Service(APNs)インフラストラクチャの更新がAdobe Campaign ClassiciOSのチャネルに影響を与えます。 iOSのプッシュチャネルの停止を回避するため、OSの構成は&#x200B;**必須**&#x200B;に変更されました。

APNsの変更に関する詳細は、このページ[を参照してください。](https://developer.apple.com/news/?id=7gx0a2lp)

**影響を受けているか**

キャンペーンを使用してiOSデバイスでプッシュ通知を送信する場合は、影響を受けます。

**更新方法**

ホストされるお客様は、次の操作は必要ありません。Adobeは既に新しいルート証明書を環境に組み込んでいます。

オンプレミス/ハイブリッドのお客様は、2021年3月29日&#x200B;**までにシームレスなトランジション**&#x200B;を確実に行えるように、設定を更新する必要があります。

[新しい証明書を組み込む方法を説明します](ios-certificate-update.md)。


## 便利なリンク

* [環境のアップグレード](../production/using/build-upgrade.md)
* [ビルドアップグレードに関する FAQ](../platform/using/faq-build-upgrade.md)
* [Campaign Classicビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)
* [新しいクライアントコンソールをユーザーが利用できるようにする](../installation/using/client-console-availability-for-windows.md)
