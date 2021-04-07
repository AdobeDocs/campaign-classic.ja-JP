---
solution: Campaign Classic
product: campaign
title: テクニカルノート
description: テクニカルノート
hide: true
hidefromtoc: true
exl-id: 7db02123-2e2a-40d9-8385-728ff69985e4
translation-type: tm+mt
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 100%

---

# Adobe Campaign 設定の更新 — 2021 年 3 月{#acc-config-updates}

インフラストラクチャと設定を定期的に更新して、最新のビルドと製品の修正を反映するようにしてください。 これらの修正は、サービスとセキュリティの継続性を確保するために必要です。 さらに、サードパーティによる変更に合わせてアップグレードする必要もあります。

アドビは、**ホステッドサービスまたはマネージドサービスのお客様**&#x200B;には、ビルドのアップグレードについて定期的に通知します。 コンプライアンスを確保するために、推奨事項に従ってアップグレードする必要があります。

**オンプレミスまたはハイブリッドのお客様**&#x200B;は、リリースされた最新のビルドに合わせて、実装を定期的にアップグレードしてください。

セキュリティ上の理由から、次に示すバージョンのいずれかにアップグレードする必要があります。 標準のアップグレード手順に加えて、環境の安全性を確保し、アドビまたはサードパーティ製システムの今後の変更に確実に対応できるように、いくつかの手動タスクも実行する必要があります。

>[!NOTE]
>
>これらの変更点に関するご質問は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。


## セキュリティの更新 {#acc-security-updates}

Campaign の最新バージョンには、サーバーサイドリクエストフォージェリ（SSRF）の問題に対する保護を強化するセキュリティ修正が適用されています。 詳しくは、[このページ](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)を参照してください。

**影響を受けていますか？**

環境が以下にリストされているものよりも低いビルドの場合は、影響を受けます。

* Gold Standard 11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース。 [詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース。 [詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース。 [詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース。 [詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース。 [詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース。 [詳細情報](../rn/using/release--19-1.md)

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

上記の新しいビルドの 1 つにアップグレードする必要があります。

* アドビは、ハイブリッドのお客様には、ミッドソーシングインスタンスのアップグレード予定日を通知します。 アドビでは、マーケティングインスタンスもアップグレードすることを強くお勧めします。

   新しいビルドは Campaign Classic 17.9 リリースと下位互換性がありますが、アドビでは、セキュリティの脆弱性に対処するために、すべてのインスタンスに対するアップグレードを強くお勧めします。

* オンプレミスのお客様は、マーケティングインスタンスとミッドソーシングインスタンスを最新ビルドにアップグレードする必要があります。

>[!CAUTION]
>
>推奨期間内にアップグレードできない場合は、**アドビカスタマーケアチームに連絡して、お使いのインスタンスに短期間の手動セキュリティ修正を適用してください**。


## Campaign Classic クライアントコンソールの更新 {#acc-cc-updates}

最近特定されたリグレッションを解決するために、**現在利用可能な**&#x200B;以下のコンソールバージョンをインストールしてください。このリグレッションにより、配信での日付選択や画像管理など、クライアントコンソールの一部のコンポーネントを使用できませんでした。 **コンソールのアップグレード**&#x200B;は必須です。

* 最新の Gold Standard 11 ビルド 9032@10c2709。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 20.1.4 リリース。 [詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース。 [詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース。 [詳細情報](../rn/using/release--19-1.md)

## Adobe Identity Management System（IMS）の更新

Adobe ID サービス（IMS）は、**2021 年 6 月 30 日**&#x200B;以降、古いバージョンの Internet Explorer のサポートを停止します。 [詳細情報](https://helpx.adobe.com/jp/x-productkb/global/update-operating-system-and-browser.html)。

Adobe IMS との互換性を確保するには、Campaign クライアントコンソールのアップグレードが必要です。

**影響がありますか？**

Adobe ID ](../integrations/using/about-adobe-id.md)経由で Campaign [に接続する場合は、Adobe Identity Management サービス（IMS）を使用して、以下の新しいバージョンのうちの1つにアップグレードする必要があります。

* Gold Standard 11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース。 [詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース。 [詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース。 [詳細情報](../rn/using/release--20-2.md)
* Campaign 20.1.4 リリース。 [詳細情報](../rn/using/release--20-1.md)
* Campaign 19.2.4 リリース。 [詳細情報](../rn/using/release--19-2.md)
* Campaign 19.1.8 リリース。 [詳細情報](../rn/using/release--19-1.md)

これらのリリースには、新しい接続プロトコルが付属しています。**2021 年 6 月 30 日**&#x200B;以降、キャンペーンサーバーとクライアントコンソールの両方が Campaign に接続できるようにするには、アップグレードが必須です。

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

ホステッドサービスのお客様には、アドビは、近日中にインスタンスを新しいバージョンにアップグレードできるようにお客様と連携して対応します。

オンプレミス／ハイブリッドのお客様は、新しいクライアントコンソール恩恵を受け、シームレスなトランジションを確保するために、**2021年6月30日までに**&#x200B;新しいバージョンの1つにアップグレードする必要があります。

すべてのインスタンスをアップグレードしたら、クライアントコンソールもこのバージョンにアップグレードする必要があります。

* [アドビのソフトウェア配布](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)へのアクセス方法を学びます。

* [Campaign クライアントコンソールのインストール方法を学びます](../installation/using/installing-the-client-console.md)。

## Experience Cloud トリガーとの統合  {#acc-triggers-updates}

従来の oAuth 認証サービスは終了しました。 トリガー統合認証は、もともとパイプラインにアクセスするための oAUTH 認証設定に基づいていましたが、Adobe I/O に移行しました。**2021 年 11 月 30 日**&#x200B;に廃止されます。 [詳細情報](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/APIEOL.md?mv=email)。

**影響がありますか？**

インスタンスが **Campaign 19.1.8、20.2.4、Gold Standard 11よりも古いバージョンで実行されている場合は**、oAuth 認証による古いバージョンのトリガー統合を使用しています。**新しいバージョンにアップグレードしてAdobe I/O に移行する必要があります**。

以下に示す新しいバージョンの1つにアップグレードする必要があります。

* Gold Standard 11。 [詳細情報](../rn/using/gold-standard.md)
* Campaign 21.1.1 リリース。 [詳細情報](../rn/using/latest-release.md)
* Campaign 20.3.3 リリース。 [詳細情報](../rn/using/release--20-3.md)
* Campaign 20.2.4 リリース。 [詳細情報](../rn/using/release--20-2.md)
* Campaign 19.1.8 リリース。 [詳細情報](../rn/using/release--19-1.md)

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

インスタンスを新しいバージョンにアップグレードしたら、すべてのお客様は、[手順に従って新しい認証モードに移行する必要があります](../integrations/using/configuring-adobe-io.md)。 この場合は、新しい Adobe I/O トークンを生成して、実装で使用する必要があります。 

さらに、ハイブリッド環境の場合、パイプラインがミッドソーシングインスタンスで設定されていることを確認する必要があります。[詳細情報](../integrations/using/configuring-pipeline.md)。

[Adobe I/O に移行する方法を説明します](../integrations/using/configuring-adobe-io.md)。

## APNs の更新  {#acc-apns-updates}

### HTTP/2 ベースの APNs プロバイダー API

Apple プッシュ通知サービス（APNs）は、**2021 年 3 月 31 日**&#x200B;をもって、従来のバイナリプロトコルをサポートしなくなります。 [詳細を表示](https://developer.apple.com/news/?id=c88acm2b)。

**影響がありますか？**

**Campaign 21.1 より古いバージョン**&#x200B;でインスタンスが実行されており、従来の Apple バイナリプロトコルでプッシュ通知を送信する場合は、HTTP/2 ベースの APNs プロバイダー API に更新する必要があります。

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

**更新方法**

ホステッドサービスのお客様が新しいビルドにアップグレードした場合、お使いのインスタンスは既に HTTP/2 ベースの API に更新されています。

オンプレミス／ホストのお客様は、設定を更新する必要があります。 [HTTP/2 への移行方法](https://helpx.adobe.com/campaign/kb/migrate-to-apns-http2.html)

### APNs ルート証明書の更新

2021年3月29日の Apple プッシュ通知サービス（APNs）インフラストラクチャの更新は、Adobe Campaign Classic iOS チャネルに影響を与えます。 iOS プッシュチャネルの停止を回避するには、OS 設定の変更が&#x200B;**必須**&#x200B;です。

APNs 変更の詳細については、[このページ](https://developer.apple.com/news/?id=7gx0a2lp)を参照してください。

**影響がありますか？**

キャンペーンを使用して iOS デバイスでプッシュ通知を送信する場合は、影響があります。

**更新方法**

ホストされているお客様は、アクションは必要ありません。アドビはすでに新しいルート証明書を環境に組み込んでいます。

オンプレミス／ハイブリッドのお客様は、シームレスなトランジションを確保するために、**2021 年 3 月 29 日までに**&#x200B;設定を更新する必要があります。

[新しい証明書を組み込む方法を説明します](ios-certificate-update.md)。

## 役立つリンク

* [環境のアップグレード](../production/using/build-upgrade.md)
* [ビルドアップグレードに関する FAQ](../platform/using/faq-build-upgrade.md)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)
* [新しいクライアントコンソールをユーザーが利用できるようにする](../installation/using/client-console-availability-for-windows.md)
