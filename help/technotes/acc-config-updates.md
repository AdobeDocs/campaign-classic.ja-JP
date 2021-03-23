---
solution: Campaign Classic
product: campaign
title: テクノテ
description: テクノテ
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 01f4e4ee841a797f4be61ffc01096b7f651ce963
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 13%

---


# Adobe Campaign構成の更新 — 2021年3月{#acc-config-updates}

インフラストラクチャと設定は定期的に更新され、最新のビルドと製品の修正が行われます。 これらの修正は、サービスとセキュリティの継続性を確保するために必要です。 さらに、サードパーティの変更と連携するために、アップグレードが必要になります。

**ホストまたはManaged Servicesのお客様**&#x200B;として、Adobeから定期的にビルドアップグレードがお知らせします。 コンプライアンスを確保するために、推奨事項に従ってアップグレードする必要があります。

**オンプレミスまたはハイブリッドのお客様**&#x200B;として、最新のリリース済みのビルドに合わせて、定期的に実装をアップグレードする必要があります。

セキュリティ上の理由から、次に示すバージョンのいずれかにアップグレードする必要があります。 標準的なアップグレード手順に加えて、環境が安全で、Adobeまたはサードパーティ製システムからの変更を今後行う準備ができるように、いくつかの手動タスクを行う必要があります。

>[!NOTE]
>
>これらの変更に関するご質問は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。


## セキュリティの更新

最新のキャンペーンバージョンには、サーバー側要求偽造(SSRF)の問題に対する保護を強化するセキュリティ修正が付属しています。 詳細[は、このページ](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)を参照してください。

**影響を受けているか**

環境の構築が下に示す構築よりも低い場合は、次の影響を受けます。

* ゴールドスタンダード11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース.[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース.[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース.[詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース.[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース.[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース.[詳細情報](../rn/using/release--19-1.md)

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

上記の新しいビルドの1つにアップグレードする必要があります。

* ハイブリッドなお客様は、ミッドソーシングインスタンスのアップグレード予定日がAdobeから通知されます。 Adobeでは、マーケティングインスタンスもアップグレードすることを強くお勧めします。

   新しいビルドは、Campaign Classic17.9リリースと下位互換性がありますが、Adobeでは、セキュリティの脆弱性に対処するために、すべてのインスタンスに対してアップグレードを推奨します

* オンプレミスのお客様は、マーケティングインスタンスとミッドソーシングインスタンスを最新のビルドにアップグレードするよう求められます。

>[!CAUTION]
>
>推奨期間内にアップグレードできない場合は、**Adobeカスタマーケアチームに連絡して、インスタンス**&#x200B;に短期間の手動セキュリティ修正を適用する必要があります。


## Campaign Classicクライアントコンソールの更新

最近識別された回帰を解決するには、次の&#x200B;**コンソールバージョン**&#x200B;をインストールする必要があります。 この問題は、配信での日付選択や画像管理など、クライアントコンソールの一部のコンポーネントが使用できなかった問題を修正しました。 **コンソール** のアップグレードは必須です。

* 最新のGold Standard 11ビルド9032@10c2709。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 20.1.4 リリース.[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース.[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース.[詳細情報](../rn/using/release--19-1.md)

## AdobeIdentity Managementシステム(IMS)の更新

AdobeIDサービス(IMS)は、**2021年6月30日**&#x200B;からの古いバージョンのInternet Explorerのサポートを停止します。 [詳細情報](https://helpx.adobe.com/x-productkb/global/update-operating-system-and-browser.html)。

AdobeIMSとの互換性を確保するには、キャンペーンクライアントコンソールのアップグレードが必要です。

**影響を受けているか**

Adobe ID](../integrations/using/about-adobe-id.md)経由でキャンペーン[に接続する場合は、AdobeIdentity Managementサービス(IMS)を使用して、以下の新しいバージョンの1つにアップグレードする必要があります。

* ゴールドスタンダード11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース.[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース.[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース.[詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース.[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース.[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース.[詳細情報](../rn/using/release--19-1.md)

これらのリリースには、新しい接続プロトコルが付属しています。**2021年6月30日**&#x200B;以降、キャンペーンサーバーとクライアントコンソールの両方がキャンペーンに接続できるようにするには、アップグレードが必須です。

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

ホスト対象のお客様は、近日中にインスタンスを新しいバージョンにアップグレードするようAdobeにご相談いたします。

オンプレミス/ハイブリッドのお客様は、新しいクライアントコンソールのメリットを活かすために、新しいバージョンの1つにアップグレードする必要があります。また、2021年6月30日&#x200B;**までにシームレスなトランジションを確保する必要があります。**

すべてのインスタンスをアップグレードしたら、クライアントコンソールもこのバージョンにアップグレードする必要があります。

* [Adobeソフトウェア配布](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)にアクセスする方法を説明します。

* [キャンペーンクライアントコンソールのインストール方法を説明します](../installation/using/installing-the-client-console.md)。

## Experience Cloudトリガーとの統合

従来のoAuth認証サービスが提供終了に達しました。 元々、パイプラインにアクセスするためのoAUTH認証設定に基づくトリガー統合認証は、Adobe I/Oに移行しました。**2021年11月30日**&#x200B;に退役します。 [詳細情報](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md?mv=email)。

**影響を受けているか**

インスタンスがキャンペーン19.1.8、20.2.4、Gold Standard 11 **より古いバージョンの**&#x200B;で実行されている場合、oAuth認証を使用して古いバージョンのトリガー統合を使用しています。**新しいバージョンにアップグレードし、Adobe I/O**&#x200B;に移動する必要があります。

以下に示す新しいバージョンの1つにアップグレードする必要があります。

* ゴールドスタンダード11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース.[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース.[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース.[詳細情報](../rn/using/release--20-2.md)
* Campaign 19.1.8 リリース.[詳細情報](../rn/using/release--19-1.md)

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

インスタンスを新しいバージョンにアップグレードしたら、すべてのお客様は、[手順に従って新しい認証モード](../integrations/using/configuring-adobe-io.md)に移行する必要があります。 これには、新しいAdobe I/Oトークンを生成し、実装で使用する必要があります。  

さらに、ハイブリッド環境の場合、パイプラインがミッドソーシングインスタンスで設定されていることを確認する必要があります。[詳細情報](../integrations/using/configuring-pipeline.md)。

[Adobe I/O に移行する方法を説明します](../integrations/using/configuring-adobe-io.md).

## APNsアップデート

### HTTP/2ベースのAPNsプロバイダーAPI

Apple Push Notification Service(APNs)は、**2021年3月31日**&#x200B;以降、レガシーバイナリプロトコルをサポートしなくなります。 [詳細を表示](https://developer.apple.com/news/?id=c88acm2b)。

**影響を受けているか**

インスタンスがキャンペーン21.1、**より古いバージョン**&#x200B;で実行され、レガシーAppleバイナリプロトコルを使用してプッシュ通知を送信する場合は、HTTP/2ベースのAPNsプロバイダーAPIに更新する必要があります。

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

ホスト対象のお客様は、新しいビルドにアップグレードした場合、Adobeは既にインスタンスをHTTP/2ベースのAPIに更新しています。

オンプレミス/ホストのお客様は、設定を更新する必要があります。 [HTTP/2への移行方法](https://helpx.adobe.com/jp/campaign/kb/migrate-to-apns-http2.html)

### APNsルート証明書の更新

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
