---
product: campaign
title: Adobe Analytics Connectorへの移行
description: Campaign - Analyticsコネクタに関するFAQ
hide: true
hidefromtoc: true
source-git-commit: cde4ed65abb2458fc40639b92314f8d56b18b78c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 9%

---

# Adobe Analytics Connectorに移行する方法 {#acc-aa-faq}

Campaign Classicv7 21.1.3リリースより、Adobe Analytics Data Connectorは非推奨（廃止予定）になります。 [詳細情報](https://experienceleague.adobe.com/docs/analytics/import/dataconnectors/data-connectors-eol.html)

2021年8月1日に、Adobe Campaign Classicは従来のData Connectors UIから削除されますが、既存のCampaign統合は引き続きデータを収集し、2022年3月1日までAdobe Analyticsに渡します。 2022年3月1日、統合は、データを収集してAdobe Analyticsに渡すのを停止します。

[このページ](../platform/using/adobe-analytics-connector.md)で説明しているように、従来のData Connectors統合に代わる、AdobeExchangeの新しいAdobe Analytics Connector統合に移行する必要があります。


>[!NOTE]
>
>これらの変更点に関するご質問は、[FAQ](#faq-aa)を参照してください。 詳しくは、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。


## 何が変わった？

Campaign Classicv7とAdobe Analyticsの新しい統合が利用できるようになりました。 主な変更点を以下に示します。

* Adobe Campaign Classic認証とAdobe Analytics認証の統合は、ユーザー/パスワードからAdobeIdentity Managementサービス(IMS)に移行しました。 そのため、Analyticsコネクタの実装を開始する前に、AdobeIMSを実装し、Adobe ID](../integrations/using/about-adobe-id.md)を介してCampaign [に接続する必要があります。

* Adobe Analyticsでは、コンタクト日&#x200B;**分類（日付タイプ）が廃止されました。**&#x200B;移行された統合では、同じタイプのままになります。 Campaignで作成される&#x200B;**コンタクト日**&#x200B;の場合、タイプは&#x200B;**文字列**&#x200B;になります。

* **処理ル** ールは、新しい統合の一部としてAdobe Campaignによって作成されます。**処理ルール**&#x200B;は、Adobe Analyticsから手動で作成するか、クライアント側JavaScript実装を直接使用する必要があります。 **処理ル** ールは、既存の統合に対してそのまま維持されます。

* 組み込みのテクニカルワークフローとその動作は変わりません。 Adobe Analyticsとの間でデータのプッシュ/プルをおこなうためにワークフローで使用されるバックエンドAPIのみが変更されました。

* 新しいコネクタを動作させるには、`nlserver`プロセスをIMSテクニカルアカウントユーザーと共に設定する必要があります。 この変更は、Adobeがおこなう必要があります。 これを実装するには、[Adobeカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

* Adobe AnalyticsからデータをプルしてプッシュするためのカスタマイズされたワークフローでAdobe Genesis APIを使用していた場合は、新しいAdobe Analytics 1.4/2.0 APIを使用する必要があります。 [詳細情報](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360047148832-Replacements-for-Data-Connector-API-calls)

## 影響の有無

既存のAdobe Analytics Data Connector(旧称：Genesis統合)を使用し、統合がCampaign 21.1.3よりも低いビルドで実装された場合は、影響を受けます。

バージョンを確認する方法については、](../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)こちらの節[を参照してください。

## 更新方法

2022年3月1日より前に、Campaign 21.1.3（またはそれ以上）の&#x200B;**にアップグレードする必要があります。**

ホスト版のお客様は、Adobeがお客様と連携して、インスタンスを新しいバージョンにアップグレードします。

オンプレミス/ハイブリッドのお客様は、新しい統合のメリットを享受するために、新しいバージョンの1つにアップグレードする必要があります。

すべてのインスタンスがアップグレードされると、新しい統合](../platform/using/adobe-analytics-connector.md)をAdobe Analytics Connectorに[実装し、シームレスな移行を確実におこなえるようになります。


## よくある質問{#faq-aa}

**ログを取得するにはどうすればよいですか？**

ユーザーインターフェイスの設定とワークフローには、**verbose**&#x200B;ログが搭載されています。

詳細モードでは、Adobe Analyticsへの各APIリクエストに対して、リクエストヘッダーと応答ヘッダーも出力されます。

オンプレミスユーザーは、次のように詳細モードを実装できます。

* ユーザーインターフェイスの詳細モードを有効にするには：詳細モードで`web`プロセスを再実行します。
* **webAnalytics**&#x200B;ワークフローの詳細モードを有効にするには：ワークフローのプロパティから「**エンジンで実行**」オプションを選択し、詳細モードで`wfserver`を再実行します。

**「統合所有者が管理者ではない」エラーが意味するエラーは何ですか？**

Data Connectorsの「Integration Owner Not Admin」エラーについて詳しくは、[このページ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360035167932-Adobe-Analytics-Data-Connectors-Integration-Owner-Not-Admin-Error)を参照してください。

**新しいコネクタへの移行が完了したら、古いデータおよびレポートスイートはどうなりますか。**

移行後、新しいコネクタ（古いコネクタから移行済み）は、同じレポートスイートへのデータのプッシュを開始し、既存のデータは影響を受けません。既存のデータに追加されます。

**Analyticsに存在する一部の既存のeVar/イベント/レポートスイートは、Campaignで表示されません。どうすればよいですか。**

統合は、日々の操作で、テクニカルアカウントトークンのデータに依存します。 テクニカルアカウントユーザーに関連付けられた製品プロファイルからディメンション/指標/レポートスイートに対する権限がない場合、使用するAPIは、単にそれらのリクエストで遅延します。

Analyticsコンポーネントの詳細（指標、ディメンション、セグメント、レポートスイートなど）を読んでいる場合、APIは、結果でこれらのコンポーネントを返しません（Analytics側で何かが削除されたか、存在しないように見える場合があります）。 Analytics APIはこれらのリクエストを拒否し、エラーアウトします。

解決策は、テクニカルユーザートークンのAnalyticsユーザーコンテキストの&#x200B;**製品プロファイル**&#x200B;を、[Adobe Admin Console](https://adminconsole.adobe.com/)に追加することで、新しく作成または欠落したコンポーネントで更新することです。 ガイダンスについて詳しくは、[Adobeカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 役立つリンク

* [環境のアップグレード](../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../platform/using/faq-build-upgrade.md)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)
* [ユーザーへの新しいクライアントコンソールの公開](../installation/using/client-console-availability-for-windows.md)
* [Campaign クライアントコンソールのインストール](../installation/using/installing-the-client-console.md)
