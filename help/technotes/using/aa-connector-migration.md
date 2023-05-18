---
product: campaign
title: Adobe Analytics Connector への移行
description: Campaign - Analytics Connector に関する FAQ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
exl-id: 5bf61654-3d68-4560-a93f-7a768a2c5be4
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: ht
source-wordcount: '858'
ht-degree: 100%

---

# 既存の Genesis 統合を Adobe Analytics Connector に移行する方法 {#acc-aa-faq}



Campaign Classic v7 21.1.3 リリース以降、Adobe Analytics Data Connector は非推奨になりました。[詳細情報](https://experienceleague.adobe.com/docs/analytics/import/dataconnectors/data-connectors-eol.html?lang=ja)

2021年8月1日（PT）、Adobe Campaign Classic は従来の Data Connectors UI から削除されましたが、既存の Campaign 統合は 2022年8月17日（PT）まで引き続きデータを収集して Adobe Analytics に渡します。この期限を過ぎると、統合によるデータの収集と Adobe Analytics への送信を停止します。

従来の Data Connectors 統合に代わる、新しい Adobe Analytics Connector 統合を Adobe Exchange に&#x200B;**実装する必要があります**。Adobe Analytics Connector について詳しくは、[このページ](../../platform/using/adobe-analytics-connector.md)を参照してください。

これらの変更点に関するご質問については、[FAQ](#faq-aa) を参照してください。 詳しくは、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

>[!NOTE]
>
>既存の Adobe Analytics Connector（旧称：Genesis 統合）から移行し、Adobe Analytics で新しい分類アーキテクチャを使用している場合、新しい Adobe Analytics Connector に移行するには、7.3.1 または 8.4.1 以降のビルドバージョンが必要です。

## 変更点

Campaign Classic v7と Adobe Analytics の間で新しい統合が利用できるようになりました。 主な変更点を以下に示します。

* Adobe Analytics では、**コンタクト日**&#x200B;分類（日付タイプ）が廃止されました。移行された統合でも、同じタイプのままです。 Campaign で作成される&#x200B;**コンタクト日**&#x200B;の場合、タイプは&#x200B;**文字列**&#x200B;になります。

* **処理ルール** は、新しい統合の一部として Adobe Campaign によって作成されます。**処理ルール**&#x200B;は、Adobe Analytics から手動で作成するか、クライアントサイド JavaScript 実装を直接使用する必要があります。 **処理ルール** は、既存の統合に対してはそのまま維持されます。

* ビルトインのテクニカルワークフローとその動作は変わりません。 Adobe Analytics との間でデータのプッシュ／プルを行うためにワークフローで使用されるバックエンド API のみ変更されました。

* 新しいコネクタを動作させるには、`nlserver`プロセスを IMS テクニカルアカウントユーザーに設定してください。この変更は、アドビで行う必要があります。 これを実装するには、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

* カスタマイズしたワークフローで Adobe Genesis API を使用して Adobe Analytics との間でデータのプッシュ／プルを行っていた場合は、新しい Adobe Analytics 1.4／2.0 API を使用する必要があります。[詳細情報](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360047148832-Replacements-for-Data-Connector-API-calls)

## 影響の有無

既存の Adobe Analytics Data Connector（旧称：Genesis 統合）を使用し、統合が Campaign 21.1.3 よりも古いビルドで実装されている場合は、影響を受けます。

バージョンを確認する方法については、](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)この節[を参照してください。

## 更新方法

**2022年8月17日（PT）までに**、Campaign 21.1.3（またはそれ以降）にアップグレードする必要があります。

ホスト環境のお客様の場合は、アドビがお客様と協力してインスタンスを新しいバージョンにアップグレードします。その後、[Adobe Analytics Connector](../../platform/using/adobe-analytics-connector.md) を使用できるようになります。

オンプレミス環境またはハイブリッド環境のお客様の場合は、新しい統合のメリットを享受するには、いずれかの新しいバージョンにアップグレードする必要があります。すべてのインスタンスがアップグレードされると、Adobe Analytics Connector に[新しい統合を実装し](../../platform/using/adobe-analytics-provisioning.md)、シームレスな移行を確実に行うことができるようになります。

## FAQ{#faq-aa}

**ログを取得するにはどうすればよいですか？**

ユーザーインターフェイス設定とワークフローは、**詳細**&#x200B;ログを備えています。

詳細モードでは、Adobe Analytics への API リクエストごとに、リクエストヘッダーと応答ヘッダーも出力されます。

オンプレミスユーザーは、次のように詳細モードを実装できます。

* ユーザーインターフェイスの詳細モードを有効にするには：詳細モードで `web` プロセスを再実行します。
* **webAnalytics** ワークフローの詳細モードを有効にするには、ワークフローのプロパティから「**エンジンで実行**」オプションを選択し、`wfserver` を詳細モードで再実行します。

**「Integration Owner Not Admin」エラーは何を意味しますか？**

コネクタの `Integration Owner Not Admin` エラーについて詳しくは、[このページ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360035167932-Adobe-Analytics-Data-Connectors-Integration-Owner-Not-Admin-Error)を参照してください。

**新しいコネクタへの移行が完了したら、古いデータおよびレポートスイートはどうなりますか？**

移行後、（古いコネクタから移行した）新しいコネクタは、同じレポートスイートへのデータのプッシュを開始しますが、既存のデータは影響を受けません。データは既存のデータに追加されます。

**Analytics に存在する一部の既存の eVar／イベント／レポートスイートは、Campaign では表示されません。 どうすればよいですか？**

日々の操作については、統合はテクニカルアカウントトークンのデータに依存します。テクニカルアカウントユーザーに関連する製品プロファイルにディメンション／指標／レポートスイートに対する権限が見当たらない場合、使用する API はそれらのリクエストに対してただ失敗するだけです。

Analytics コンポーネント（指標、ディメンション、セグメント、レポートスイートなど）の詳細について読み取っている場合、API は、結果にこれらのコンポーネントを返しません（Analytics 側で何かが削除されたか存在しないように見えます）。Analytics API はこれらのリクエストを拒否し、エラーになります。

解決策としては、[Adobe Admin Console](https://adminconsole.adobe.com/){_blank} で新しく作成するか、不足しているコンポーネントを追加して、そのコンポーネントでテクニカルユーザートークンの Analytics ユーザーコンテキストの&#x200B;**製品プロファイル**&#x200B;を更新することです。詳しくは、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 参考になるリンク

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html)
* [ユーザーへの新しいクライアントコンソールの公開](../../installation/using/client-console-availability-for-windows.md)
* [Campaign クライアントコンソールのインストール](../../installation/using/installing-the-client-console.md)
