---
product: campaign
title: プライバシー
description: プライバシーに関するベストプラクティスの詳細を説明します
feature: URL Personalization, Privacy
exl-id: 0a3473bf-0528-486d-a799-8db86fece522
source-git-commit: 197ac1322cb8f4f34d2670a29d622a21f407c90c
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 33%

---

# プライバシー {#privacy}

![](../../assets/v7-only.svg)

## プライバシーリクエスト

Adobe Campaign には、GDPR および CCPA に則ってプライバシーを遵守するのに役立つ一連のツールが用意されています。

参照： [このページ](../../platform/using/privacy-management.md) プライバシー管理の概要とAdobe Campaignの実装手順に関する一般的な情報を参照してください。 また、ベストプラクティスや、ユーザープロセスとペルソナの概要も確認できます。

## URL のパーソナライゼーション {#url-personalization}

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを回避するために、URL のホスト名部分にパーソナライゼーションを含めないようにしてください。 次の例は、すべての URL 属性 &lt;`a href="">` または `<img src="">` で使用しないでください。

* `<%= url >`
* `https://<%= url >`
* `https://<%= domain >/path`
* `https://<%= sub-domain >.domain.tld/path`
* `https://sub.domain<%= main domain %>/path`

### レコメンデーション

上記を使用していないことを検証し確認するには、を使用してトラッキング URL テーブルに対してクエリを実行します。 [キャンペーン汎用クエリエディター](../../platform/using/steps-to-create-a-query.md) または [クエリアクティビティ](../../workflow/using/query.md).

例：

1. ワークフローの作成と **クエリ** アクティビティ。 [詳細情報](../../workflow/using/query.md)。

1. を開きます。 **クエリ** アクティビティを作成し、 `nmsTrackingUrl` 表を次に示します。

   `source URL starts with http://<% or source URL starts with https://<%`

1. ワークフローを実行し、結果があるかを確認します。

1. 結果がある場合は、出力トランジションを開いて URL のリストを表示します。

   ![](assets/privacy-query-dynamic-url.png)


### URL 署名

セキュリティを強化するために、E メール内のリンクを追跡するための署名メカニズムが導入されました。 これは、ビルド 19.1.4(9032@3a9dc9c) および 20.2 以降で使用できます。この機能は、デフォルトで有効になっています。

>[!NOTE]
>
>不正な形式の署名済み URL がクリックされると、次のエラーが返されます。 `Requested URL '…' was not found.`

また、拡張機能を使用して、以前のビルドで生成された URL を無効にすることができます。 この機能は、デフォルトでは無効になっています。 次の場所に移動して、 [カスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) この機能を有効にするには、をクリックします。

19.1.4 ビルドで実行している場合、トラッキングリンクを使用したプッシュ通知配信、またはアンカータグを使用した配信で問題が発生する可能性があります。 その場合は、URL 署名を無効にすることをお勧めします。

Campaign がホストする、管理対象Cloud Services、ハイブリッド顧客は、 [カスタマーケア](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) URL 署名を無効にする。

ハイブリッドアーキテクチャで Campaign を実行している場合は、URL 署名を有効にする前に、ホストされているミッドソーシングインスタンスが次のようにアップグレードされていることを確認します。

* まず、オンプレミスマーケティングインスタンスを使用します
* その後、オンプレミスのマーケティングインスタンスと同じバージョンにアップグレードするか、少し高いバージョンにアップグレードします

そうしないと、次の問題が発生する可能性があります。

* ミッドソーシングインスタンスがアップグレードされる前は、このインスタンスを通じて URL が署名なしで送信されます。
* ミッドソーシングインスタンスをアップグレードし、両方のインスタンスで URL 署名が有効になった後、以前に署名なしで送信された URL は拒否されます。 これは、マーケティングインスタンスから提供されたトラッキングファイルによって署名が要求されたためです。

以前のビルドで生成された URL を無効にするには、すべての Campaign サーバーで同時に次の手順に従います。

1. サーバー設定ファイル (`serverConf.xml`)、 **blockRedirectForUnsignedTrackingLink** 選択肢 **true**.
1. を再起動します。 `nlserver` サービス。
1. の `tracking` サーバー、再起動 `web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）。

URL 署名を有効にするには、すべての Campaign サーバーで同時に次の手順に従います。

1. サーバー設定ファイル (`serverConf.xml`)、変更 **signEmailLinks** オプション、 **true**.
1. **nlserver** サービスを再起動します。
1. の `tracking` サーバー、再起動 `web` サーバー（Debian では apache2、CentOS/RedHat では httpd、Windows では IIS）。

## データの制限

権限の低い認証済みユーザーは、暗号化されたパスワードにアクセスできないようにする必要があります。 これをおこなうには、パスワードフィールドのみ、またはエンティティ全体（ビルド >= 8770 が必要）へのアクセスを制限します。

この制限をおこなうと、パスワードフィールドを削除する一方で、外部アカウントは全ユーザー向けのインターフェイスからアクセス可能にできます。[詳細情報](../../configuration/using/restricting-pii-view.md)。

手順は次のとおりです。

1. 次を参照： **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]** Campaign エクスプローラーのフォルダー。

1. としてのデータスキーマの作成 **[!UICONTROL スキーマの拡張]**.

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
   >次を置換： `$(loginId) = 0 or $(login) = 'admin'` と `hasNamedRight('admin')` 管理者権限を持つすべてのユーザーに対し、これらのパスワードの表示を許可する。

## PI を持つProtectページ

オンプレミス版のお客様には、ミラーページや Web アプリケーションなど、個人情報 (PI) を含む可能性のあるページを保護することを強くお勧めします。

この手順の目的は、これらのページのインデックス化を防止することによってセキュリティリスクを回避することです。以下に、この目的に役立つ記事をいくつか示します。

* [https://developers.google.com/search/reference/robots_txt](https://developers.google.com/search/reference/robots_txt)
* [https://developers.google.com/search/reference/robots_meta_tag](https://developers.google.com/search/reference/robots_meta_tag)

ページを保護するには、次の手順に従います。

1. Web サーバー（Apache または IIS）のルートに `robots.txt` ファイルを追加します。このファイルの内容は次のとおりです。

   ```sql
   # Make changes for all web spiders
   User-agent:
   *Disallow: /
   ```

   IIS の場合は、 [このページ](https://docs.microsoft.com/en-us/iis/extensions/iis-search-engine-optimization-toolkit/managing-robotstxt-and-sitemap-files).

   Apache の場合は、にファイルを配置できます。 **/var/www/robots.txt** (Debian)。

1. 場合によっては、 **robots.txt** ファイルはセキュリティの点で十分ではありません。 例えば、他の Web サイトに自社ページへのリンクがある場合は、検索結果に自社ページの情報が表示される可能性があります。

   **robots.txt** ファイルに加え、**X-Robots-Tag** ヘッダーも追加することをお勧めします。Apache の場合も IIS の場合も、このヘッダーの追加は **serverConf.xml** 設定ファイルでおこなえます。

   詳しくは、 [この記事](https://developers.google.com/search/reference/robots_meta_tag).
