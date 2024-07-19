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

上記を使用していないことを検証および確認するには、[Campaign 汎用クエリエディター ](../../platform/using/steps-to-create-a-query.md) でトラッキング URL テーブルに対してクエリを実行するか、[ クエリアクティビティ ](../../workflow/using/query.md) でフィルター条件を使用してワークフローを作成します。

例：

1. ワークフローを作成し、**クエリ** アクティビティを追加します。 [詳細情報](../../workflow/using/query.md)。

1. **クエリ** アクティビティを開き、`nmsTrackingUrl` テーブルに次のようにフィルターを作成します。

   `source URL starts with http://<% or source URL starts with https://<%`

1. ワークフローを実行し、結果があるかを確認します。

1. 結果がある場合は、出力トランジションを開いて URL のリストを表示します。

   ![](assets/privacy-query-dynamic-url.png)


### URL 署名

セキュリティを向上させるために、メール内のリンクをトラッキングするための署名メカニズムが導入されました。 ビルド 19.1.4 （9032@3a9dc9c）および 20.2 以降で使用できます。この機能はデフォルトで有効になっています。

>[!NOTE]
>
>不正な形式の署名済み URL をクリックすると、次のエラーが返されます。`Requested URL '…' was not found.`

さらに、機能強化を使用して、以前のビルドで生成された URL を無効にすることができます。 この機能は、デフォルトでは無効になっています。 この機能を有効にする方法については、[ カスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) にお問い合わせください。

ビルド 19.1.4 を実行している場合、トラッキングリンクを使用したプッシュ通知配信や、アンカータグを使用した配信で問題が発生する可能性があります。 その場合は、URL 署名を無効にすることをお勧めします。

Campaign がホストするマネージドCloud Serviceまたはハイブリッドのお客様は、URL 署名を無効にするには、[ カスタマーケア ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) に連絡する必要があります。

ハイブリッドアーキテクチャで Campaign を実行している場合、URL 署名を有効にする前に、ホストされているミッドソーシングインスタンスが次のようにアップグレードされていることを確認します。

* 最初に、オンプレミスマーケティングインスタンス
* その後、オンプレミスマーケティングインスタンスと同じバージョンまたは少し新しいバージョンにアップグレードします

そうしないと、次のような問題が発生する場合があります。

* ミッドソーシングインスタンスがアップグレードされる前に、このインスタンスを通じて URL が署名なしで送信されます。
* ミッドソーシングインスタンスがアップグレードされ、両方のインスタンスで URL 署名が有効になると、以前に署名なしで送信された URL は拒否されます。 その理由は、マーケティングインスタンスから提供されたトラッキングファイルによって署名がリクエストされるからです。

以前のビルドで生成された URL を無効にするには、すべての Campaign サーバーで次の手順を同時に実行します。

1. サーバー設定ファイル（`serverConf.xml`）で、「**blockRedirectForUnsignedTrackingLink**」オプションを **true** に変更します。
1. `nlserver` サービスを再起動します。
1. `tracking` サーバーで、`web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）を再起動します。

URL 署名を有効にするには、すべての Campaign サーバーで次の手順を同時に実行します。

1. サーバー設定ファイル（`serverConf.xml`）で、「**signEmailLinks**」オプションを **true** に変更します。
1. **nlserver** サービスを再起動します。
1. `tracking` サーバーで、`web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）を再起動します。

## データの制限

権限の低い認証ユーザーが、暗号化されたパスワードにアクセスできないようにする必要があります。 それには、パスワードフィールドのみへのアクセス、またはエンティティ全体へのアクセスを制限します（ビルド >= 8770 が必要）。

この制限をおこなうと、パスワードフィールドを削除する一方で、外部アカウントは全ユーザー向けのインターフェイスからアクセス可能にできます。[詳細情報](../../configuration/using/restricting-pii-view.md)。

手順は次のとおりです。

1. Campaign エクスプローラーの **[!UICONTROL 管理]**/**[!UICONTROL 設定]**/**[!UICONTROL データスキーマ]** フォルダーを参照します。

1. データスキーマを、**[!UICONTROL スキーマの拡張]** として作成します。

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
   >`$(loginId) = 0 or $(login) = 'admin'` を `hasNamedRight('admin')` に置き換えて、管理者権限を持つすべてのユーザーにこれらのパスワードを表示させることができます。

## PI を使用したProtectページ

オンプレミスのお客様には、ミラーページ、web アプリケーションなどの個人情報（PI）を含む可能性のあるページを保護することを強くお勧めします。

この手順の目的は、これらのページのインデックスが作成されないようにすることで、潜在的なセキュリティリスクを回避することです。 以下に、この目的に役立つ記事をいくつか示します。

* [https://developers.google.com/search/reference/robots_txt](https://developers.google.com/search/reference/robots_txt)
* [https://developers.google.com/search/reference/robots_meta_tag](https://developers.google.com/search/reference/robots_meta_tag)

ページを保護するには、次の手順に従います。

1. Web サーバーのルート（Apache または IIS）に `robots.txt` ファイルを追加します。 このファイルの内容は次のとおりです。

   ```sql
   # Make changes for all web spiders
   User-agent:
   *Disallow: /
   ```

   IIS については、[ このページ ](https://docs.microsoft.com/en-us/iis/extensions/iis-search-engine-optimization-toolkit/managing-robotstxt-and-sitemap-files) を参照してください。

   Apache の場合、ファイルを **/var/www/robots.txt** （Debian）に配置できます。

1. **robots.txt** ファイルを追加しても、セキュリティの点で十分でない場合があります。 例えば、他の Web サイトに自社ページへのリンクがある場合は、検索結果に自社ページの情報が表示される可能性があります。

   **robots.txt** ファイルに加えて、**X-Robots-Tag** ヘッダーを追加することをお勧めします。 Apache または IIS と、**serverConf.xml** 設定ファイルで実行できます。

   詳しくは、[ この記事 ](https://developers.google.com/search/reference/robots_meta_tag) を参照してください。


## プライバシーリクエスト

Privacy Management の概要とAdobe Campaignでの実装手順について詳しくは、[ このページ ](../../platform/using/privacy-management.md) を参照してください。 また、ベストプラクティス、ユーザープロセスとペルソナの概要についても説明します。
