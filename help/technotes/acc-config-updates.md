---
solution: Campaign Classic
product: campaign
title: テクニカルノート
description: テクニカルノート
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: bdd746120f2162cf48eeb9d519513656bd4e75aa
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 58%

---


# Adobe Campaign 設定のアップグレード - 2021 年 3 月 {#acc-config-updates}

インフラストラクチャと設定は定期的に更新され、最新のビルドと製品の修正が行われます。 これらの修正は、サービスとセキュリティの継続性を確保するために必要です。 さらに、サードパーティの変更と連携するために、アップグレードが必要になります。

**ホストまたはManaged Servicesのお客様**&#x200B;として、Adobeから定期的にビルドアップグレードがお知らせします。 コンプライアンスを確保するために、推奨事項に従ってアップグレードする必要があります。

**オンプレミスまたはハイブリッドのお客様**&#x200B;として、最新のリリース済みのビルドに合わせて、定期的に実装をアップグレードする必要があります。

セキュリティ上の理由から、次に示すバージョンのいずれかにアップグレードする必要があります。 標準的なアップグレード手順に加えて、環境が安全で、Adobeまたはサードパーティ製システムからの変更を今後行う準備ができるように、いくつかの手動タスクを行う必要があります。

>[!NOTE]
>
>これらの変更に関するご質問は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。


## セキュリティの更新 {#acc-security-updates}

最新のキャンペーンバージョンには、サーバー側要求偽造(SSRF)の問題に対する保護を強化するセキュリティ修正が付属しています。 詳しくは、[このページ](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)を参照してください。

**影響を受けていますか**

環境が以下にリストされているものよりも下位のビルドの場合、影響を受けます。

* Gold Standard 11[詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース[詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース[詳細情報](../rn/using/release--19-1.md)

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

上記の新しいビルドの いずれかにアップグレードする必要があります。

* ハイブリッドなお客様は、ミッドソーシングインスタンスのアップグレード予定日がAdobeから通知されます。 Adobeでは、マーケティングインスタンスもアップグレードすることを強くお勧めします。

   新しいビルドは、Campaign Classic17.9リリースと下位互換性がありますが、Adobeでは、セキュリティの脆弱性に対処するために、すべてのインスタンスに対してアップグレードを推奨します

* オンプレミスのお客様は、マーケティングインスタンスとミッドソーシングインスタンスを最新のビルドにアップグレードするよう求められます。

>[!CAUTION]
>
>推奨期間内にアップグレードできない場合は、**Adobeカスタマーケアチームに連絡して、インスタンス**&#x200B;に短期間の手動セキュリティ修正を適用する必要があります。


## Campaign Classicクライアントコンソールの更新{#acc-cc-updates}

最近識別された回帰を解決するには、次の&#x200B;**コンソールバージョン**&#x200B;をインストールする必要があります。 この問題は、配信での日付選択や画像管理など、クライアントコンソールの一部のコンポーネントが使用できなかった問題を修正しました。 **コンソールのアップグレードは必須です。**

* 最新のGold Standard 11ビルド9032@10c2709。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 20.1.4 リリース[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース[詳細情報](../rn/using/release--19-1.md)

## Adobe Identity Management System（IMS）のアップデート

AdobeIDサービス(IMS)は、**2021年6月30日**&#x200B;からの古いバージョンのInternet Explorerのサポートを停止します。 [詳細情報](https://helpx.adobe.com/x-productkb/global/update-operating-system-and-browser.html)。

AdobeIMSとの互換性を確保するには、キャンペーンクライアントコンソールのアップグレードが必要です。

**影響の有無**

dobe Identity Management サービス（IMS）を使用し、](../integrations/using/about-adobe-id.md)Adobe ID 経由[で Campaign に接続している場合は、以下にリストされている新しいバージョンのいずれかにアップグレードする必要があります。

* Gold Standard 11[詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース[詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース[詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース[詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース[詳細情報](../rn/using/release--19-1.md)

このリリースでは新しい接続プロトコルを使用しています。**2021 年 6 月 30 日**&#x200B;以降、Campaign サーバーとクライアントコンソールの両方を Campaign に接続するには、アップグレードが必須です。

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

ホスト対象のお客様は、近日中にインスタンスを新しいバージョンにアップグレードするようAdobeにご相談いたします。

オンプレミス／ハイブリッドのお客様は、新しいクライアントコンソールから恩恵を受け、シームレスにトランジションできるように、**2021 年 6 月 30 日までに**&#x200B;新しいバージョンのいずれかにアップグレードする必要があります。

すべてのインスタンスをアップグレードしたら、クライアントコンソールもこのバージョンにアップグレードする必要があります。

* [アドビのソフトウェア配布](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=jp)へのアクセス方法

* [Campaign クライアントコンソールのインストール方法](../installation/using/installing-the-client-console.md)

## Experience Cloud トリガーとの統合  {#acc-triggers-updates}

従来の OAuth 認証サービスは終了しました。 トリガー統合認証は、もともと OAuth 認証設定に基づいてパイプラインにアクセスしていましたが、Adobe I/O に移行しました。トリガー統合認証は、**2021 年 11 月 30 日**&#x200B;に廃止されます。[詳細情報](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md?mv=email)。

**影響の有無**

インスタンスが **Campaign 19.1.8、20.2.4、Gold Standard 11 より古いバージョン**&#x200B;で実行されている場合、OAuth 認証による古いバージョンのトリガー統合を使用しています。**新しいバージョンにアップグレードして、Adobe I/O に移行する必要があります**。

以下に示す新しいバージョンのいずれかにアップグレードする必要があります。

* Gold Standard 11[詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース[詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース[詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース[詳細情報](../rn/using/release--20-2.md)
* Campaign 19.1.8 リリース[詳細情報](../rn/using/release--19-1.md)

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

インスタンスを新しいバージョンにアップグレードしたら、すべてのお客様は、 [手順に従って新しい認証モードに移行](../integrations/using/configuring-adobe-io.md)する必要があります。これには、新しいAdobe I/Oトークンを生成し、実装で使用する必要があります。  

さらに、ハイブリッド環境の場合、パイプラインがミッドソーシングインスタンスで設定されていることを確認する必要があります。[詳細情報](../integrations/using/configuring-pipeline.md)。

[Adobe I/O に移行する方法を説明します](../integrations/using/configuring-adobe-io.md)。

## APN アップデート  {#acc-apns-updates}

### HTTP/2 ベースの APN プロバイダー API

Apple Push Notification Service（APN）は、 **2021 年 3 月 31 日以降、**&#x200B;従来のバイナリプロトコルをサポートしなくなります。[詳細を表示](https://developer.apple.com/news/?id=c88acm2b)。

**影響を受けている場合**

インスタンスがキャンペーン21.1、**より古いバージョン**&#x200B;で実行され、レガシーAppleバイナリプロトコルを使用してプッシュ通知を送信する場合は、HTTP/2ベースのAPNsプロバイダーAPIに更新する必要があります。

この節](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)で、バージョン[を確認する方法を説明します。

**更新方法**

ホスト対象のお客様は、新しいビルドにアップグレードした場合、Adobeは既にインスタンスをHTTP/2ベースのAPIに更新しています。

オンプレミス／ホストのお客様は、設定を更新する必要があります。 [HTTP/2 への移行方法](https://helpx.adobe.com/jp/campaign/kb/migrate-to-apns-http2.html)

### APN ルート証明書のアップデート

2021 年 3 月 29 日、Apple Push Notification Service（APN）インフラストラクチャのアップデートが Adobe Campaign Classic iOS チャネルに影響を与えます。iOS のプッシュチャネルの停止を回避するには、OS 設定の変更が&#x200B;**必須**&#x200B;です。

APNs 変更の詳細については、 [こちらのページ](https://developer.apple.com/news/?id=7gx0a2lp)を参照してください。

**影響の有無**

Campaign を使用して iOS デバイスでプッシュ通知を送信している場合は、影響を受けます。

**更新方法**

アクションは必要ありません。アドビはすでに新しいルート証明書を環境に組み込んでいます。

オンプレミス／ハイブリッドのお客様は、シームレスにトランジションできるよう、**2021 年 3 月 29 日までに**&#x200B;設定を更新する必要があります。

[新しい証明書を組み込む方法を説明します](ios-certificate-update.md)。

## 役立つリンク

* [環境のアップグレード](../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../platform/using/faq-build-upgrade.md)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)
* [新しいクライアントコンソールをユーザーが利用できるようにする](../installation/using/client-console-availability-for-windows.md)
