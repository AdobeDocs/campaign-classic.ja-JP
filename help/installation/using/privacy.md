---
product: campaign
title: パーソナライゼーションとプライバシー
description: プライバシーとパーソナライゼーションのセキュリティに関するベストプラクティス
feature: Installation, Privacy, Privacy Tools, URL Personalization
exl-id: 0a3473bf-0528-486d-a799-8db86fece522
TQID: 'https://experienceleague.adobe.com/8u-ItsbouC0wIsamVYfyzQR1o-z-jY90Z3pKem-yarc'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a7760dfc-5c44-4d77-bb68-c50b1e265c93
    internal-label: Security and privacy
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
    internal-label: Prepare and test messages
subfeature_v2:
  - id: ac72e249-ebbf-4bb6-96c9-596af925419a
    internal-label: Privacy tools
  - id: ac9c0a9c-8a76-4419-bd64-9c34c5782666
    internal-label: Privacy
  - id: fb2a841f-c522-491f-9901-a1b939d252df
    internal-label: Security
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
  - id: f55cfb22-471c-4161-8ea1-12868351e460
    internal-label: URL personalization
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: 758d5159759b19f7ef32e8cc8f6237547599e727
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 29%
---
# パーソナライゼーションとプライバシー {#privacy}

このページでは、URLのパーソナライゼーション、URL署名、個人情報を含むページの保護について説明します。

>[!NOTE]
>
>Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 データ制限とプライバシー要求について詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/privacy/security#data-restriction){target=_blank}を参照してください。
>
>[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/privacy/security#data-restriction){target=_blank}

Campaign Classic v7では、エンティティ全体へのアクセスを制限するには、ビルド 8770以降が必要です。

## URL のパーソナライゼーション {#url-personalization}

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを回避するために、URL のホスト名部分にパーソナライゼーションを含めないようにしてください。 次の例は、すべての URL 属性 &lt;`a href="">` または `<img src="">` で使用しないでください。

* `<%= url >`
* `https://<%= url >`
* `https://<%= domain >/path`
* `https://<%= sub-domain >.domain.tld/path`
* `https://sub.domain<%= main domain %>/path`

### レコメンデーション

上記を使用していないことを検証して確認するには、[Campaign汎用クエリエディター](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/data/query/query-editor){target="_blank"} （Campaign v8 ドキュメント）を介してトラッキング URL テーブルでクエリを実行するか、クエリアクティビティでフィルター条件を使用するワークフローを作成します。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/query.html?lang=ja){target="_blank"}を参照してください。

例：

1. ワークフローを作成し、**クエリ** アクティビティを追加します。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/query.html?lang=ja){target="_blank"}を参照してください。

1. **クエリ** アクティビティを開き、次のように`nmsTrackingUrl` テーブルにフィルターを作成します。

   `source URL starts with http://<% or source URL starts with https://<%`

1. ワークフローを実行し、結果があるかを確認します。

1. 結果がある場合は、出力トランジションを開いて URL のリストを表示します。

   ![](assets/privacy-query-dynamic-url.png)


### URL署名

セキュリティを強化するため、メール内のリンクを追跡するための署名メカニズムが導入されました。 ビルド 19.1.4 （9032@3a9dc9c）および20.2以降で使用できます。 この機能はデフォルトで有効になっています。

>[!NOTE]
>
>形式が正しくない署名済みURLをクリックすると、このエラーが返されます：`Requested URL '…' was not found.`

さらに、機能強化を使用して、以前のビルドで生成されたURLを無効にすることもできます。 この機能はデフォルトで無効になっています。 この機能を有効にするには、[ カスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

19.1.4 ビルドで実行している場合、トラッキングリンクを使用したプッシュ通知の配信やアンカータグを使用した配信で問題が発生する可能性があります。 その場合は、URL署名を無効にすることをお勧めします。

Campaign ホスト版、Managed Cloud Servicesまたはハイブリッド版のお客様の場合、URL署名を無効にするには、[ カスタマーケア ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。

ハイブリッドアーキテクチャでCampaignを実行している場合は、URL署名を有効にする前に、ホストされているミッドソーシングインスタンスが次のようにアップグレードされていることを確認します。

* まず、オンプレミスマーケティングインスタンスは
* 次に、オンプレミスマーケティングインスタンスと同じバージョンに、または少し高いバージョンにアップグレードします

それ以外の場合、次のような問題が発生する可能性があります。

* ミッドソーシングインスタンスをアップグレードする前に、このインスタンスを介して署名なしでURLが送信されます。
* ミッドソーシングインスタンスがアップグレードされ、両方のインスタンスでURL署名が有効になると、署名なしで以前に送信されたURLが拒否されます。 その理由は、マーケティングインスタンスによって提供されたトラッキングファイルによって署名が要求されるためです。

以前のビルドで生成されたURLを無効にするには、すべてのCampaign サーバーで同時に次の手順に従います。

1. サーバー設定ファイル （`serverConf.xml`）で、**blockRedirectForUnsignedTrackingLink** オプションを&#x200B;**true**&#x200B;に変更します。
1. `nlserver` サービスを再起動します。
1. `tracking` サーバーで、`web` サーバー（Debianではapache2、CentOS/RedHatではhttpd、WindowsではIIS）を再起動します。

URL署名を有効にするには、すべてのCampaign サーバーで同時に次の手順に従います。

1. サーバー設定ファイル （`serverConf.xml`）で、**signEmailLinks** オプションを&#x200B;**true**&#x200B;に変更します。
1. **nlserver** サービスを再起動します。
1. `tracking` サーバーで、`web` サーバー（Debianではapache2、CentOS/RedHatではhttpd、WindowsではIIS）を再起動します。

## PIでページを保護

ミラーページ、web アプリケーションなどの個人情報（PI）を含む可能性のあるページを保護することをオンプレミスのお客様に強くお勧めします。

この手順の目的は、これらのページのインデックス作成を防ぎ、潜在的なセキュリティリスクを回避することです。 以下に、この目的に役立つ記事をいくつか示します。

* [https://developers.google.com/search/reference/robots_txt](https://developers.google.com/search/reference/robots_txt)
* [https://developers.google.com/search/reference/robots_meta_tag](https://developers.google.com/search/reference/robots_meta_tag)

ページを保護するには、次の手順に従います。

1. Web サーバー（ApacheまたはIIS）のルートに`robots.txt` ファイルを追加します。 このファイルの内容は次のとおりです。

   ```sql
   # Make changes for all web spiders
   User-agent:
   *Disallow: /
   ```

   IISについては、[このページ ](https://docs.microsoft.com/en-us/iis/extensions/iis-search-engine-optimization-toolkit/managing-robotstxt-and-sitemap-files)を参照してください。

   Apacheの場合は、**/var/www/robots.txt** （Debian）にファイルを配置できます。

1. **robots.txt** ファイルを追加するだけでは、セキュリティの観点から不十分な場合があります。 例えば、他の Web サイトに自社ページへのリンクがある場合は、検索結果に自社ページの情報が表示される可能性があります。

   **robots.txt** ファイルに加えて、**X-Robots-Tag** ヘッダーを追加することをお勧めします。 ApacheまたはIISと&#x200B;**serverConf.xml**&#x200B;設定ファイルで実行できます。

   詳しくは、[この記事](https://developers.google.com/search/reference/robots_meta_tag)を参照してください。
