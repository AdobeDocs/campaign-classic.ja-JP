---
solution: Campaign Classic
product: campaign
title: プライバシー
description: プライバシーに関するベストプラクティスの詳細を参照してください。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 768fe62db4efd1217c22973c7e5dc31097d67bae
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 53%

---


# プライバシー {#privacy}

## プライバシーリクエスト

Adobe Campaign には、GDPR および CCPA に則ってプライバシーを遵守するのに役立つ一連のツールが用意されています。

プライバシー管理の概要とAdobe Campaignの導入手順については、[このページ](../../platform/using/privacy-management.md)を参照してください。 また、ベストプラクティスや、ユーザープロセスと個人の概要も確認できます。

## URL のパーソナライゼーション {#url-personalization}

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを避けるために、URL の hostname 部分はパーソナライズしないでください。次の例は、すべてのURL属性&lt;`a href="">`または`<img src="">`で使用しないでください。

* `<%= url >`
* `https://<%= url >`
* `https://<%= domain >/path`
* `https://<%= sub-domain >.domain.tld/path`
* `https://sub.domain<%= main domain %>/path`

### レコメンデーション

上記を検証して使用していないことを確認するには、[キャンペーン汎用クエリエディター](../../platform/using/steps-to-create-a-query.md)を介して追跡URLテーブルに対してクエリを実行するか、[クエリアクティビティ](../../workflow/using/query.md)でフィルタ条件を使用してワークフローを作成します。

例：

1. ワークフローを作成し、クエリアクティビティを追加します。 詳細情報.

1. クエリアクティビティを開き、次のようにnmsTrackingUrlテーブルにフィルターを作成します。ソースURL開始ーにhttp://&lt;%を使用するか、ソースURL開始ーにhttps://&lt;%を使用します。

1. ワークフローを実行し、結果があるかを確認します。

1. 結果がある場合は、出力トランジションを開いて URL のリストを表示します。

<img src="assets/privacy-query-dynamic-url.png">

### 署名のメカニズム

セキュリティを強化するため、電子メールのリンクを追跡するための新しい署名メカニズムは、ビルド19.1.4(9032@3a9dc9c)で導入され、ビルド19.1.4(9032@3a9dc9c)およびキャンペーン20.2で利用できます。このオプションは、すべてのお客様に対してデフォルトで有効です。

>[!NOTE]
>
>不正な形式の署名済み URL がクリックされると、次のエラーが返されます。「リクエストされた URL &#39;...&#39; が見つかりませんでした。」

また、キャンペーン20.2およびゴールド標準リリースから、ホストおよびハイブリッドのお客様は、拡張機能を使用して以前のビルドで生成されたURLを無効にできます。 このオプションはデフォルトでは無効です。この機能を有効にするには、[カスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

オンプレミス環境でこの新しいメカニズムを有効にするには、すべての Campaign サーバーで次の手順を実行する必要があります。

1. サーバー設定ファイル（serverConf.xml）で、**blockRedirectForUnsignedTrackingLink** を **true** に変更します。
1. **nlserver** サービスを再起動します。
1. トラッキングサーバーで、Webサーバー（Debianではapache2、CentOS/RedHatではhttpd、WindowsではIIS）を再起動します。

Gold Standard 19.1.4を使用している場合、トラッキングリンクを使用するプッシュ通知配信またはアンカータグを使用する配信で問題が発生する可能性があります。 その場合、Adobeでは、リンクの追跡に使用する新しい署名メカニズムを無効にすることをお勧めします。

**ホストおよびハイブリッド** のお客様は、 [カスタマー](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) ケアに連絡して、このメカニズムを無効にする必要があります。

**オンプレミスの** 顧客は、次の手順に従います。

1. サーバー設定ファイル(serverConf.xml)で、**signEmailLinks**&#x200B;を&#x200B;**false**&#x200B;に変更します。
1. **nlserver** サービスを再起動します。
1. トラッキングサーバーで、Webサーバー（Debianではapache2、CentOS/RedHatではhttpd、WindowsではIIS）を再起動します。

## データの制限

権限レベルの低い認証ユーザーは暗号化されたパスワードにアクセスできないようにする必要があります。これを実現するには、主に 2 つの方法があります。パスワードフィールドへのアクセスを制限する方法と、エンティティ全体へのアクセスを制限する方法です（ビルド 8770 以降が必要です）。

この制限をおこなうと、パスワードフィールドを削除する一方で、外部アカウントは全ユーザー向けのインターフェイスからアクセス可能にできます。[このページ](../../configuration/using/restricting-pii-view.md)を参照してください。

1. **[!UICONTROL 管理]**／**[!UICONTROL 設定]**／**[!UICONTROL データスキーマ]**&#x200B;に移動します。

1. 新しい&#x200B;**[!UICONTROL スキーマの拡張]**&#x200B;を作成します。

   ![](assets/privacy-data-restriction.png)

1. **[!UICONTROL 外部アカウント]**（extAccount）を選択します。

1. 最後のウィザード画面で、新しい srcSchema を編集して、すべてのパスワードフィールドへのアクセスを制限します。

   メイン要素(`<element name="extAccount" ... >`)は、次の方法で置き換えることができます。

   ```
   <element name="extAccount">
       <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
       <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
   
       <element name="s3Account">
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="awsSecret"/>
       </element>
       <element name="wapPush">
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
       </element>
       <element name="mms">
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
       </element>
   </element>
   ```

   拡張されたsrcSchemaは次のようになります。

   ```
   <srcSchema _cs="External Accounts (cus)" created="2017-05-12 07:53:49.691Z" createdBy-id="0"
               desc="Definition of external accounts (Email, SMS...) used by the modules"
               entitySchema="xtk:srcSchema" extendedSchema="nms:extAccount" img="" label="External Accounts"
               labelSingular="External account" lastModified="2017-05-12 08:33:49.365Z"
               mappingType="sql" md5="E9BB0CD6A4375F500027C86EA854E101" modifiedBy-id="0"
               name="extAccount" namespace="cus" xtkschema="xtk:srcSchema">
       <createdBy _cs="Administrator (admin)"/>
       <modifiedBy _cs="Administrator (admin)"/>
       <element name="extAccount">
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
           <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
   
           <element name="s3Account">
               <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="awsSecret"/>
           </element>
           <element name="wapPush">
               <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
               <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
           </element>
           <element name="mms">
               <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="password"/>
               <attribute accessibleIf="$(loginId) = 0 or $(login) = 'admin'" name="clientSecret"/>
           </element>
       </element>
   </srcSchema>    
   ```

   >[!NOTE]
   >
   >`$(loginId) = 0 or $(login) = 'admin'`を`hasNamedRight('admin')`で削除すると、管理者権限を持つすべてのユーザーにこれらのパスワードを表示できます。

## PII を含むページの保護

オンプレミス版のお客様の場合は、ミラーページや Web アプリケーションのように、個人情報を含む可能性があるページを保護することを強くお勧めします。

この手順の目的は、これらのページのインデックス化を防止することによってセキュリティリスクを回避することです。以下に、この目的に役立つ記事をいくつか示します。

* [https://developers.google.com/search/reference/robots_txt](https://developers.google.com/search/reference/robots_txt)
* [https://developers.google.com/search/reference/robots_meta_tag](https://developers.google.com/search/reference/robots_meta_tag)
* [https://www.google.com/webmasters/tools/robots-testing-tool](https://www.google.com/webmasters/tools/robots-testing-tool)

ページを保護するには、次の手順に従います。

1. Web サーバー（Apache または IIS）のルートに robots.txt ファイルを追加します。このファイルの内容は次のとおりです。

   ```
   # Make changes for all web spiders
   User-agent:
   *Disallow: /
   ```

   IISの場合は、[このページ](https://docs.microsoft.com/en-us/iis/extensions/iis-search-engine-optimization-toolkit/managing-robotstxt-and-sitemap-files)を参照してください。

   Apacheの場合は、ファイルを&#x200B;**/var/www/robots.txt** (Debian)に配置できます。

1. **robots.txt**&#x200B;ファイルを追加するのは、セキュリティ上十分ではないことがあります。 例えば、他の Web サイトに自社ページへのリンクがある場合は、検索結果に自社ページの情報が表示される可能性があります。

**robots.txt** ファイルに加え、**X-Robots-Tag** ヘッダーも追加することをお勧めします。Apache の場合も IIS の場合も、このヘッダーの追加は **serverConf.xml** 設定ファイルでおこなえます。

詳しくは、[この記事](https://developers.google.com/search/reference/robots_meta_tag)を参照してください。
