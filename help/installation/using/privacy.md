---
product: campaign
title: パーソナライゼーションとプライバシー
description: プライバシーとパーソナライゼーションに関するセキュリティのベストプラクティスについて説明します
feature: Installation, Privacy, Privacy Tools, URL Personalization
exl-id: 0a3473bf-0528-486d-a799-8db86fece522
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 20%

---

# パーソナライゼーションとプライバシー {#privacy}

## URL のパーソナライゼーション {#url-personalization}

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを回避するために、URL のホスト名部分にパーソナライゼーションを含めないようにしてください。 次の例は、すべての URL 属性 &lt;`a href="">` または `<img src="">` で使用しないでください。

* `<%= url >`
* `https://<%= url >`
* `https://<%= domain >/path`
* `https://<%= sub-domain >.domain.tld/path`
* `https://sub.domain<%= main domain %>/path`

### レコメンデーション

上記を使用していないことを検証および確認するには、以下を介してトラッキング URL テーブルに関するクエリを実行します [Campaign 汎用クエリエディター](../../platform/using/steps-to-create-a-query.md) または、でフィルター条件を使用してワークフローを作成します [クエリアクティビティ](../../workflow/using/query.md).

例：

1. ワークフローを作成して追加 **クエリ** アクティビティ。 [詳細情報](../../workflow/using/query.md)。

1. を開きます **クエリ** アクティビティを選択し、 `nmsTrackingUrl` 次の表を参照してください。

   `source URL starts with http://<% or source URL starts with https://<%`

1. ワークフローを実行し、結果があるかを確認します。

1. 結果がある場合は、出力トランジションを開いて URL のリストを表示します。

   ![](assets/privacy-query-dynamic-url.png)


### URL 署名

セキュリティを向上させるために、メール内のリンクをトラッキングするための署名メカニズムが導入されました。 ビルド 19.1.4 （9032@3a9dc9c）および 20.2 以降で使用できます。この機能はデフォルトで有効になっています。

>[!NOTE]
>
>不正な形式の署名済み URL をクリックすると、次のエラーが返されます。 `Requested URL '…' was not found.`

さらに、機能強化を使用して、以前のビルドで生成された URL を無効にすることができます。 この機能は、デフォルトでは無効になっています。 にお問い合わせください。 [カスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) ：この機能を有効にします。

ビルド 19.1.4 を実行している場合、トラッキングリンクを使用したプッシュ通知配信や、アンカータグを使用した配信で問題が発生する可能性があります。 その場合は、URL 署名を無効にすることをお勧めします。

Campaign がホストするマネージドCloud Serviceまたはハイブリッドのお客様は、次の URL にアクセスする必要があります。 [カスタマーケア](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) で URL 署名を無効にします。

ハイブリッドアーキテクチャで Campaign を実行している場合、URL 署名を有効にする前に、ホストされているミッドソーシングインスタンスが次のようにアップグレードされていることを確認します。

* 最初に、オンプレミスマーケティングインスタンス
* その後、オンプレミスマーケティングインスタンスと同じバージョンまたは少し新しいバージョンにアップグレードします

そうしないと、次のような問題が発生する場合があります。

* ミッドソーシングインスタンスがアップグレードされる前に、このインスタンスを通じて URL が署名なしで送信されます。
* ミッドソーシングインスタンスがアップグレードされ、両方のインスタンスで URL 署名が有効になると、以前に署名なしで送信された URL は拒否されます。 その理由は、マーケティングインスタンスから提供されたトラッキングファイルによって署名がリクエストされるからです。

以前のビルドで生成された URL を無効にするには、すべての Campaign サーバーで次の手順を同時に実行します。

1. サーバー設定ファイル（`serverConf.xml`）、を変更します。 **blockRedirectForUnsignedTrackingLink** 対するオプション **true**.
1. を再起動します `nlserver` サービス。
1. 日 `tracking` サーバー、を再起動する `web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）。

URL 署名を有効にするには、すべての Campaign サーバーで次の手順を同時に実行します。

1. サーバー設定ファイル（`serverConf.xml`）、変更 **signEmailLinks** オプション、終了#オプション ツイカ# **true**.
1. **nlserver** サービスを再起動します。
1. 日 `tracking` サーバー、を再起動する `web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）。

## データの制限

権限の低い認証ユーザーが、暗号化されたパスワードにアクセスできないようにする必要があります。 それには、パスワードフィールドのみへのアクセス、またはエンティティ全体へのアクセスを制限します（ビルド >= 8770 が必要）。

この制限をおこなうと、パスワードフィールドを削除する一方で、外部アカウントは全ユーザー向けのインターフェイスからアクセス可能にできます。[詳細情報](../../configuration/using/restricting-pii-view.md)。

手順は次のとおりです。

1. を参照してください。 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]** campaign エクスプローラーのフォルダー。

1. データスキーマを **[!UICONTROL スキーマの拡張]**.

   ![](assets/privacy-data-restriction.png)

1. **[!UICONTROL 外部アカウント]**（extAccount）を選択します。

1. ウィザードの最後の画面で、新しい「srcSchema」を編集して、すべてのパスワードフィールドへのアクセスを制限します。

   メイン要素（`<element name="extAccount" ... >`）は、次の方法で置き換えることができます。

   ```sql
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

   したがって、拡張された srcSchema は次のようになります。

   ```sql
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
   >次を置換できます `$(loginId) = 0 or $(login) = 'admin'` （を使用） `hasNamedRight('admin')` 管理者権限を持つすべてのユーザーにこれらのパスワードの表示を許可します。

## PI を使用したProtectページ

オンプレミスのお客様には、ミラーページ、web アプリケーションなどの個人情報（PI）を含む可能性のあるページを保護することを強くお勧めします。

この手順の目的は、これらのページのインデックスが作成されないようにすることで、潜在的なセキュリティリスクを回避することです。 以下に、この目的に役立つ記事をいくつか示します。

* [https://developers.google.com/search/reference/robots_txt](https://developers.google.com/search/reference/robots_txt)
* [https://developers.google.com/search/reference/robots_meta_tag](https://developers.google.com/search/reference/robots_meta_tag)

ページを保護するには、次の手順に従います。

1. を追加 `robots.txt` web サーバーのルートにあるファイル（Apache または IIS）。 このファイルの内容は次のとおりです。

   ```sql
   # Make changes for all web spiders
   User-agent:
   *Disallow: /
   ```

   IIS については、次を参照してください [このページ](https://docs.microsoft.com/en-us/iis/extensions/iis-search-engine-optimization-toolkit/managing-robotstxt-and-sitemap-files).

   Apache の場合、ファイルは次の場所に配置できます。 **/var/www/robots.txt** （Debian）。

1. 場合によっては、 **robots.txt** ファイルはセキュリティの点で十分ではありません。 例えば、他の Web サイトに自社ページへのリンクがある場合は、検索結果に自社ページの情報が表示される可能性があります。

   に加えて **robots.txt** ファイルの場合は、を追加することをお勧めします **X-Robots-Tag** ヘッダー。 Apache または IIS と、で設定できます。 **serverConf.xml** 設定ファイル。

   詳しくは、次を参照してください。 [この記事](https://developers.google.com/search/reference/robots_meta_tag).


## プライバシーリクエスト

こちらを参照してください [このページ](../../platform/using/privacy-management.md) プライバシー管理の概要とAdobe Campaignの実装手順に関する一般的な情報について説明します。 また、ベストプラクティス、ユーザープロセスとペルソナの概要についても説明します。
