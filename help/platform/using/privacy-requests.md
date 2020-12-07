---
solution: Campaign Classic
product: campaign
title: プライバシーリクエスト
description: プライバシーリクエストの管理方法について説明します
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '2591'
ht-degree: 100%

---


# プライバシーリクエストの管理 {#privacy-requests}

プライバシー管理に関する一般的なプレゼンテーションについては、[こちら](../../platform/using/privacy-management.md)を参照してください。

この情報は、GDPR、CCPA、PDPA、LGPD に適用されます。これらの規制について詳しくは、[こちら](../../platform/using/privacy-management.md#privacy-management-regulations)を参照してください。

個人情報の販売のオプトアウト（CCPA に特有）については、[こちら](#sale-of-personal-information-ccpa)を参照してください。

>[!IMPORTANT]
>
>このドキュメントで説明されているインストール手順は Campaign Classic 18.4（ビルド 8931 以降）以降に適用されます。以前のバージョンを使用している場合は、この[テクニカルノート](https://helpx.adobe.com/jp/campaign/kb/how-to-install-gdpr-package-on-legacy-versions.html)を参照してください。

## プライバシーリクエストについて {#about-privacy-requests}

Adobe Campaign では、プライバシー対応の一環として、アクセスリクエストと削除リクエストの処理が可能です。**アクセス権利**&#x200B;および&#x200B;**忘れ去られる権利**（削除リクエスト）については[こちら](../../platform/using/privacy-management.md#right-access-forgotten)で説明しています。

ここでは、アクセスリクエストと削除リクエストの作成方法および Adobe Campaign での処理方法について説明します。

### 原則 {#principles}

Adobe Campaign では、データ管理者は 2 とおりの方法でプライバシーのアクセスリクエストおよび削除リクエストをおこなうことができます。

* **Adobe Campaign インターフェイス**&#x200B;を使用する：データ管理者はプライバシーリクエストごとに Adobe Campaign で新しいプライバシーリクエストを作成できます。[こちらの節](#create-privacy-request-ui)を参照してください。
* **API** を使用する：Adobe Campaign の API により、SOAP を使用してプライバシーリクエストを自動処理できます。[こちらの節](#automatic-privacy-request-api)を参照してください。

>[!NOTE]
>
>個人データおよびデータを管理する様々なエンティティ（データ管理者、データ処理者、データ主体）について詳しくは、[個人データとペルソナ](../../platform/using/privacy-and-recommendations.md#personal-data)を参照してください。

### 前提条件 {#prerequesites}

Adobe Campaign には、Adobe Campaign に保存されているデータに対するプライバシーリクエストの作成と処理をおこなうためのデータ管理者用ツールが用意されています。ただし、データ主体とのやり取り（電子メール、カスタマーサポート、Web ポータル）はデータ管理者がおこなう必要があります。

また、要求者であるデータ主体の身元の確認、および要求者に返されるデータがデータ主体に関するものであることの確認は、データ管理者がおこないます。

### プライバシーパッケージのインストール {#install-privacy-package}

この機能を使用するには、**[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL パッケージをインポート]**／**[!UICONTROL Adobe Campaign パッケージ]**&#x200B;メニューから&#x200B;**[!UICONTROL プライバシーデータ保護規則]**&#x200B;パッケージをインストールする必要があります。パッケージのインストール方法について詳しくは、[詳細ドキュメント](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**&#x200B;に、プライバシー専用の 2 つのフォルダーが新しく作成されます。

* **[!UICONTROL プライバシーリクエスト]**：プライバシーリクエストを作成し、その推移をトラッキングする場所です。
* **[!UICONTROL 名前空間]**：Adobe Campaign データベースでデータ主体を識別するために使用するフィールドを定義する場所です。

![](assets/privacy-folders.png)

**[!UICONTROL 管理]**／**[!UICONTROL プロダクション]**／**[!UICONTROL テクニカルワークフロー]**&#x200B;で、プライバシーリクエストを処理するための 3 つのテクニカルワークフローが毎日実行されます。

![](assets/privacy-workflows.png)

* **[!UICONTROL プライバシーリクエストを収集]**：このワークフローでは、Adobe Campaign に保存されている受信者のデータを生成し、プライバシーリクエストの画面でダウンロードできるようにします。
* **[!UICONTROL プライバシーリクエストデータを削除]**：このワークフローでは、Adobe Campaign に保存されている受信者のデータを削除します。
* **[!UICONTROL プライバシーリクエストのクリーンアップ]**：このワークフローでは、90 日より古いアクセスリクエストファイルが消去されます。

**[!UICONTROL 管理]**／**[!UICONTROL アクセス管理]**／**[!UICONTROL ネームド権限]**&#x200B;に、**[!UICONTROL プライバシーデータ権限]**&#x200B;というネームド権限が追加されました。このネームド権限は、データ管理者がプライバシーツールを使用する場合に必要となります。これにより、新しいリクエストの作成、推移のトラッキング、API の使用などができるようになります。

![](assets/privacy-right.png)

### 名前空間 {#namesspaces}

プライバシーリクエストを作成する前に、使用する名前空間を定義する必要があります。これは、Adobe Campaign データベースでデータ主体を識別するために使用するキーです。

標準では、E メール、電話、携帯電話の 3 つの名前空間を使用できます。別の名前空間（受信者用のカスタムフィールドなど）が必要な場合、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 名前空間]**&#x200B;で新しく作成することができます。

## プライバシー要求の作成 {#create-privacy-request-ui}

**Adobe Campaign インターフェイス**&#x200B;では、プライバシーリクエストを作成し、その推移をトラッキングできます。新しいプライバシーリクエストを作成するには、次の手順に従います。

1. **[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL プライバシーリクエスト]**&#x200B;のプライバシーリクエストフォルダーにアクセスします。

   ![](assets/privacy-requests-folder.png)

1. この画面では、現在のすべてのプライバシーリクエストとそのステータス、ログを表示できます。新しいプライバシーリクエストを作成するには、「**[!UICONTROL 新規]**」をクリックします。

   ![](assets/privacy-request-new.png)

1. **[!UICONTROL 規制]**（GDPR、CCPA、PDPA、LGPD）、**[!UICONTROL リクエストタイプ]**（アクセスまたは削除）、**[!UICONTROL 名前空間]**&#x200B;を選択し、**[!UICONTROL 紐付け値]**&#x200B;を入力します。名前空間として E メールを使用する場合は、データ主体の E メールアドレスを入力します。

   ![](assets/privacy-request-properties.png)

プライバシーのテクニカルワークフローは毎日 1 回実行され、新しいリクエストが個別に処理されます。

* 削除リクエスト：Adobe Campaign に保存されている受信者のデータが消去されます。
* アクセスリクエスト：Adobe Campaign に保存されている受信者のデータが生成され、リクエスト画面の左側で XML ファイルとして取得できるようになります。

![](assets/privacy-request-download.png)

### テーブルのリスト {#list-of-tables}

プライバシーに関連する削除またはアクセスリクエストの実行時に、受信者テーブル（独自タイプ）にリンクされたすべてのテーブルの&#x200B;**[!UICONTROL 紐付け値]**&#x200B;に基づいて、データ主体のすべてのデータを検索します。

以下は、プライバシーリクエストの実行時に考慮される標準テーブルをリストしたものです。

* 受信者（recipient）
* 受信者配信ログ（broadLogRcp）
* 受信者トラッキングログ（trackingLogRcp）
* アーカイブしたイベント配信ログ（broadLogEventHisto）
* 受信者リストのコンテンツ（rcpGrpRel）
* 訪問者オファー提案（propositionVisitor）
* 訪問者（visitor）
* 購読履歴（subHisto）
* 購読（subscription）
* 受信者のオファーの提案（propositionRcp）

受信者テーブル（独自タイプ）にリンクされるカスタムテーブルを作成した場合は、そのテーブルも考慮されます。例えば、受信者テーブルにリンクしているトランザクションテーブルと、そのトランザクションテーブルにリンクしているトランザクション詳細テーブルがある場合、両方のテーブルが考慮されます。

>[!IMPORTANT]
>
>プロファイル削除ワークフローを使用してプライバシーバッチリクエストを実行する場合は、次の注意点を考慮に入れてください。
>* ワークフローを使用したプロファイル削除では、子テーブルが処理されません。
>* すべての子テーブルに対して削除処理をおこなう必要があります。
>* プライバシーアクセステーブル内で削除する行を追加する ETL ワークフローを作成し、**[!UICONTROL プライバシー要求データの削除]**&#x200B;ワークフローで削除を実行することをお勧めします。パフォーマンス上の理由から、削除するプロファイルの数は 1 日あたり 200 個までに制限することをお勧めします。


### プライバシーリクエストのステータス {#privacy-request-statuses}

プライバシーリクエストには、次のようなステータスがあります。

* **[!UICONTROL 新規]**／**[!UICONTROL 再試行待ち]**：ワークフローは進行中で、リクエストの処理は完了していません。
* **[!UICONTROL 処理中]**／**[!UICONTROL 再試行中]**：ワークフローはリクエストを処理しています。
* **[!UICONTROL 削除待ち]**：ワークフローにおいて、削除対象のすべての受信者データが特定済みです。
* **[!UICONTROL 削除中]**：ワークフローは削除を処理しています。
* **[!UICONTROL 削除確認待ち]**：（2 段階処理モードの削除リクエスト）ワークフローでアクセスリクエストの処理が完了しました。削除を実行するための手動確認がリクエストされています。ボタンは 15 日間有効です。
* **[!UICONTROL 完了]**：リクエストの処理が終了しました。エラーは発生していません。
* **[!UICONTROL エラー]**：ワークフローにおいて、エラーが発生しました。理由は、プライバシーリクエストのリストの「**[!UICONTROL リクエストのステータス]**」列に表示されます。例えば、「**[!UICONTROL エラー: データが見つかりません]**」は、データ主体の&#x200B;**[!UICONTROL 紐付け値]**&#x200B;と一致する受信者データがデータベースに見つからなかったことを示します。

### 2 段階プロセス{#two-step-process}

デフォルトでは、**2 段階プロセス**&#x200B;が有効になっています。このモードで新しい削除リクエストを作成した場合、必ずアクセスリクエストが先に実行されます。これにより、削除前にデータを確認することができます。

このモードはプライバシーリクエスト編集画面から変更できます。「**[!UICONTROL 詳細設定]**」をクリックします。

![](assets/privacy-request-advanced-settings.png)

2 段階モードが有効になっていると、新しい削除リクエストのステータスは「**[!UICONTROL 削除確認待ち]**」に変わります。生成された XML ファイルをプライバシーリクエスト画面からダウンロードし、データを確認します。データの消去を確定するには、「**[!UICONTROL データの削除を確認]**」ボタンをクリックします。

![](assets/privacy-request-delete-data.png)

### JSSP URL {#jspp-url}

Adobe Campaign は、アクセスリクエストの処理時に JSSP を生成します。この JSSP は、データベースから受信者のデータを取得し、ローカルマシンに保存されている XML ファイルにエクスポートします。JSSP の URL は次のように定義されます。

```
"$(serverUrl)+'/nms/gdpr.jssp?id='+@id"
```

ここで、@id はプライバシーリクエスト ID です.

この URL は、プライバシーリクエスト（gdprRequest）スキーマの&#x200B;**[!UICONTROL 「ファイルの場所」（@urlFile）]**&#x200B;フィールドに保存されます。****

この情報はデータベースで 90 日間有効です。テクニカルワークフローによりリクエストがクリーンアップされると、この情報はデータベースから削除され、URL は無効になります。データを Web ページからダウンロードする前に、URL がまだ有効であるか確認してください。

データ主体のデータファイルの例を以下に示します。

![](assets/privacy-access-file.png)

データ管理者は JSSP URL が含まれる Web アプリケーションを簡単に作成できます。これにより、データ主体のデータファイルを Web ページから使用できるようになります。

![](assets/privacy-gdpr-jssp.png)

Web アプリケーションの&#x200B;**[!UICONTROL ページ]**&#x200B;アクティビティで例として使用できるコードスニペットを以下に示します。

![](assets/privacy-page-activity.png)

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <meta http-equiv="Content-Language" content="en"> <meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> <link rel="stylesheet" type="text/css" href="/nl/webForms/landingPage.css"/> <title>Clickthrough</title> <style type="text/css" media="all"> /* override formulary area */ .formulary { top: 200px; position: absolute; left: 0; } </style> </head> <body style="" class="">
<center>
<div id="wrap">
<div id="header"><img class="nlui-widget" alt="placeholder_header" src="/nms/img/contentModels/placeholder_header.png" unselectable="on" />
<div class="header-title center-title">DOWNLOAD GDPR DATA</div>
<div class="formulary center-formulary"><form>
<div class="button large-button"><a href=[SERVER_URL]/nms/gdpr.jssp?id=13000" data-nl-type="externalLink">CLICK TO DOWNLOAD</a></div>
</form></div>
</div>
<div id="content">
<div class="row">
<div class="info">
<div class="desc">
<div class="title">EFFICIENCY</div>
<div class="desc">Our service is guaranteed to improve your efficiency. Increase performance and use our high-technology service to implement even the most ambitious of projects.</div>
</div>
</div>
</div>
</div>
<div id="footer">
<div style="text-align: center;">
<div style="float: left;"><a href="#">Contact us</a></div>
<div style="float: right;">&copy; Copyrights</div>
<div><a href="#"><img title="facebook" class="nlui-widget" alt="facebook" src="/xtk/img/facebook.png" unselectable="on" /></a> <a href="#"><img title="Twitter" class="nlui-widget" alt="twitter" src="/xtk/img/twitter.png" unselectable="on" /></a> <a href="#"><img title="Google" class="nlui-widget" alt="google_plus" src="/xtk/img/google_plus.png" unselectable="on" /></a> <a href="#"><img title="Linkedin" class="nlui-widget" alt="Linkedin" src="/xtk/img/linkedin.png" unselectable="on" /></a></div>
</div>
</div>
</div>
</center>
</body> </html>
```

データ主体のデータファイルへのアクセスは制限されているため、Web ページへの匿名アクセスは無効にする必要があります。**[!UICONTROL プライバシーデータ権限]**&#x200B;ネームド権限があるオペレーターだけが、ページにログオンしてデータをダウンロードすることができます。

## 自動プライバシーリクエストプロセス {#automatic-privacy-request-api}

Adobe Campaign には、プライバシーリクエストの自動プロセスを設定できる **API** があります。

この API を使用した場合の一般的なプライバシープロセスは、[インターフェイスを使用](#create-privacy-request-ui)した場合と変わりません。ただし、プライバシーリクエストの作成のみが異なります。Adobe Campaign でリクエストを作成するかわりに、リクエスト情報を含む POST が Campaign に送信されます。リクエストごとに、新しいエントリが&#x200B;**[!UICONTROL プライバシーリクエスト]**&#x200B;画面に追加されます。その後、プライバシーのテクニカルワークフローにおいてリクエストが処理されます。これもインターフェイスからリクエストを追加した場合と変わりません。

API を使用してプライバシーリクエストを送信する場合、最初の削除リクエストについては、返されるデータをテストできるよう、**2 段階プロセス**&#x200B;を有効にしておくことをお勧めします。テストが終了したら、削除リクエストプロセスが自動的に実行されるよう、2 段階プロセスを無効にできます。

**[!UICONTROL CreateRequestByName]** JS API は次のように定義されます。

>[!NOTE]
>
>**gdprRequest** API を使用していた場合は引き続き使用できますが、新しい **privacyRequest** API を使用することをお勧めします。

>[!IMPORTANT]
>
>この API を使用するには、**[!UICONTROL プライバシーデータ権限]**&#x200B;ネームド権限が必要です。

```
<method library="nms:gdpr.js" name="CreateRequestByName" static="true">
 <help>Create a new GDPR Request using namespace internal name</help>
 <parameters>
  <param name="namespaceName" type="string" desc="Namespace internal name"/>
  <param name="reconciliationValue" type="string" desc="Reconciliation value"/>
  <param name="type" type="long" desc="Reconciliation value"/>
  <param name="confirmDeletePending" type="boolean" desc="Request confirm before deleting data"/>
  <param name="regulation" type="long" desc="regulation of newly created request"/>
  <param name="id" type="long" inout="out" desc="ID of newly created request"/>
 </parameters>
</method>
```

>[!NOTE]
>
>「regulation」フィールドは、Campaign Classic 20.2（ビルド 9178 以降）を使用している場合にのみ使用可能です。
>
>20.2 に移行しており既に API を使用している場合は、上記のように「regulation」フィールドを追加する必要があります。以前のビルドを使用している場合は、「regulation」フィールドなしで API を引き続き使用できます。

### 外部からの API の呼び出し {#invoking-api-externally}

外部から API を呼び出す方法の例（具体的には API を使用した認証と、プライバシー API の詳細）を以下に示します。プライバシー API について詳しくは、[API のドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/s-nms-privacyRequest.html)を参照してください。また、[Web サービス呼び出しに関するドキュメント](../../configuration/using/web-service-calls.md)も参照してください。

最初に、API を通じて認証を実行する必要があります。

1. URL「**`<server url>`/nl/jsp/schemawsdl.jsp?schema=xtk:session**」から **xtk:session** WSDL をダウンロードします。

1. &quot;Logon&quot; メソッドを使用し、リクエストのパラメーターとしてユーザー名とパスワードを渡します。セッショントークンを含む応答が返されます。SoapUI を使用する場合の例を以下に示します。

   ![](assets/privacy-api.png)

1. 返されたセッショントークンを後続のすべての API 呼び出しの認証として使用します。これは 24 時間後に有効期限切れになります。

次に、プライバシー API を呼び出します。

1. URL **`<server url>`/nl/jsp/schemawsdl.jsp?schema=nms:privacyRequest** を使用して、WSDL をダウンロードします。

1. **[!UICONTROL CreateRequestByName]** を使用して、特定のプライバシーリクエストを作成します。

   **[!UICONTROL CreateRequestByName]** を使用する場合の例を以下に示します。上記で提供されたセッショントークンを認証として使用する方法に注目してください。応答は、作成されたリクエストの ID になります。

   ![](assets/privacy-api-2.png)

   上記の手順を実行するためには、以下の点を考慮してください。

   * **nms:gdprRequest** スキーマで **queryDef** を使用すると、アクセスリクエストのステータスを確認できます。
   * **nms:gdprRequestData** スキーマで queryDef **を使用すると、アクセスリクエストの結果を取得できます。**
   * **$(serverUrl)&#39;/nms/gdpr.jssp?id=&#39;@id** から XML ファイルをダウンロードするには、許可リスト登録済みの IP からログインしてファイルにアクセスする必要があります。これをおこなうには、JSSP で生成されたファイルにアクセスできる Web アプリケーションを作成します。

### JS からの API の呼び出し {#invoking-api-from-js}

Campaign Classic 内で JS から API を呼び出す方法の例を以下に示します。

>[!NOTE]
>
>「regulation」フィールドは、Campaign Classic 20.2（ビルド 9178 以降）を使用している場合にのみ使用可能です。
>
>20.2 に移行しており、既に API を使用している場合は、「regulation」フィールドを追加する必要があります。以前のビルドを使用している場合は、「regulation」フィールドなしで API を引き続き使用できます。

* **以前のビルドを GDPR パッケージと一緒に使用**&#x200B;している場合、下記のように「regulation」フィールドなしで API を引き続き使用できます。

   ```
   loadLibrary("nms:gdpr.js");
   /**************************** 
   This code calls an API to create new Privay request on the DB.
   It requires 4 parameters below.
   Feel free to change parameter values.
   ****************************/
   // 1. Namespace internal name
   var namespaceName = "defaultNamespace1";
   // 2. Reconciliation value for privacy request
   var reconciliationValue = "example@adobe.com";
   // 3. Privacy request type
   // GDPR_REQUEST_TYPE_ACCESS = 1;
   // GDPR_REQUEST_TYPE_DELETE = 2;
   var requestType = GDPR_REQUEST_TYPE_ACCESS;
   // 4. Confirm deleting data required.
   // value : true or false
   var ConfirmDeletePending = true;
   // BEGIN
   var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending);
   // User can use a simple queryDef with requestID as a parameter to check request status.
   ```

* **20.2 に移行**&#x200B;しており、既に API を使用している場合は、下記のように「regulation」フィールドを追加する必要があります。

   ```
   loadLibrary("nms:gdpr.js");
   /**************************** 
   This code calls an API to create new Privay request on the DB.
   It requires 5 parameters below.
   Feel free to change parameter values.
   ****************************/
   // 1. Namespace internal name
   var namespaceName = "defaultNamespace1";
   // 2. Reconciliation value for privacy request
   var reconciliationValue = "example@adobe.com";
   // 3. Privacy request type
   // PRIVACY_REQUEST_TYPE_ACCESS = 1;
   // PRIVACY_REQUEST_TYPE_DELETE = 2;
   var requestType = PRIVACY_REQUEST_TYPE_ACCESS;
   // 4. Confirm deleting data required.
   // value : true or false
   var ConfirmDeletePending = true;
   // 5. Specify which regulation applies to newly created request. This is mandatory parameter.
   // GDPR = 1
   // CCPA = 2
   // PDPA = 3
   // LGPD = 4
   var regulation = 1;
   // BEGIN
   var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending, regulation);
   // User can use a simple queryDef with requestID as a parameter to check request status.
   ```

* **Campaign Classic 20.2（ビルド 9178 以降）以降を使用**&#x200B;している場合は、下記のように「regulation」フィールドはオプションです。

   ```
   loadLibrary("nms:gdpr.js");
   /**************************** 
   This code calls an API to create new Privay request on the DB.
   It requires 5 parameters below.
   Feel free to change parameter values 
   ****************************/
   // 1. Namespace internal name
   var namespaceName = "defaultNamespace1";
   // 2. Reconciliation value for privacy request
   var reconciliationValue = "example@adobe.com";
   // 3. Privacy request type
   // PRIVACY_REQUEST_TYPE_ACCESS = 1;
   // PRIVACY_REQUEST_TYPE_DELETE = 2;
   var requestType = PRIVACY_REQUEST_TYPE_ACCESS;
   // 4. Confirm deleting data required.
   // value : true or false
   var ConfirmDeletePending = true;
   // 5. Specify which regulation applies to newly created request. This is optional parameter.
   // GDPR = 1
   // CCPA = 2
   // PDPA = 3
   // LGPD = 4
   var regulation = 1;
   // BEGIN
   var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending, regulation);
   // User can use a simple queryDef with requestID as a parameter to check request status.
   ```

## 個人情報の販売のオプトアウト（CCPA）{#sale-of-personal-information-ccpa}

**カリフォルニア州消費者プライバシー法**（CCPA）は、カリフォルニア州民に個人情報に関する新しい権利を提供し、カリフォルニア州でビジネスをおこなう特定の事業者に対してデータ保護の責任を課します。

アクセスリクエストおよび削除リクエストの設定および使用方法は、GDPR と CCPA で共通です。ここでは、CCPA に固有の個人データ販売のオプトアウトについて説明します。

Adobe Campaign が提供する[同意管理](../../platform/using/privacy-management.md#consent-management)ツールに加えて、消費者が個人情報の販売をオプトアウトしたかどうかをトラッキングすることもできます。

消費者が自分の個人情報を、システムを通じて第三者に売り渡すことを許可しないことにします。Adobe Campaign では、この情報を保存してトラッキングできます。

これをおこなうには、プロファイルテーブルを拡張して、「**[!UICONTROL CCPA のオプトアウト]**」フィールドを追加する必要があります。

>[!IMPORTANT]
>
>データ主体のリクエストを受け取り、CCPA のリクエスト日を追跡するのは、データ管理者の責任です。アドビは、テクノロジープロバイダーとして、オプトアウトの方法を提供するだけです。データ管理者としての役割について詳しくは、「[個人データとペルソナ](../../platform/using/privacy-and-recommendations.md#personal-data)」を参照してください。

### 前提条件{#ccpa-prerequisite}

この情報を活用するには、Adobe Campaign Classic でこのフィールドを作成する必要があります。この場合、**[!UICONTROL 受信者]**&#x200B;テーブルにブール値フィールドを追加します。新しいフィールドが作成されると、Campaign API によって自動的にサポートされます。

また、カスタム受信者テーブルを使用する場合、この操作を実行する必要があります。

新しいフィールドの作成方法について詳しくは、[スキーマエディションのドキュメント](../../configuration/using/about-schema-edition.md)を参照してください。

>[!IMPORTANT]
>
>スキーマの変更は機密性の高い操作であり、エキスパートユーザーのみが実行する必要があります。

1. **[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL 新しいフィールドを追加]**&#x200B;をクリックし、**[!UICONTROL 受信者]**&#x200B;を「**[!UICONTROL ドキュメントタイプ]**」として選択して、「**[!UICONTROL 次へ]**」をクリックします。テーブルへのフィールドの追加について詳しくは、[こちら](../../configuration/using/new-field-wizard.md)を参照してください。

   ![](assets/privacy-ccpa-1.png)

1. 「**[!UICONTROL フィールドタイプ]**」で「**[!UICONTROL SQL フィールド]**」を選択します。ラベルには、「**[!UICONTROL CCPA のオプトアウト]**」を使用します。**[!UICONTROL 8 ビット整数（ブール値）]**&#x200B;タイプを選択して、一意の&#x200B;**[!UICONTROL 相対パス]**「@OPTOUTCCPA」を定義します。「**[!UICONTROL 完了]**」をクリックします。

   ![](assets/privacy-ccpa-2.png)

   これにより、**[!UICONTROL 受信者（cus）]**&#x200B;スキーマが拡張または作成されます。フィールドが正しく追加されていることを確認するには、これをクリックします。

   ![](assets/privacy-ccpa-3.png)

1. エクスプローラーの&#x200B;**[!UICONTROL 設定]**／**[!UICONTROL 入力フォーム]**&#x200B;ノードをクリックします。**[!UICONTROL 受信者（nms）]**&#x200B;の「一般的なパッケージ」で、`<input>` 要素を追加して、xpath 値に、手順 2 で定義した相対パスを使用します。フォームの識別について詳しくは、[こちら](../../configuration/using/identifying-a-form.md)を参照してください。

   ```
   <input  colspan="2" type="checkbox" xpath="@OPTOUTCCPA"/>
   ```

   ![](assets/privacy-ccpa-4.png)

1. 接続を解除し、再接続します。次の節で説明する手順に従って、受信者の詳細でフィールドが使用可能であることを確認します。

### 使用状況 {#usage}

フィールドの値を入力し、データ販売に関する CCPA ガイドラインおよびルールに従うことは、データ管理者の責務となります。

値はいくつかの方法で入力できます。

* Campaign のインターフェイスを使用した受信者の詳細の編集
* API の使用
* データインポートワークフローの使用

次に、オプトアウトしたプロファイルの個人情報を第三者に販売しないようにする必要があります。

1. オプトアウトステータスを変更するには、**[!UICONTROL プロファイルとターゲット]**／**[!UICONTROL 受信者]**&#x200B;で、受信者を選択します。「**[!UICONTROL 一般]**」タブには、前の節で設定したフィールドが表示されます。

   ![](assets/privacy-ccpa-5.png)

1. 受信者リストを設定して、オプトアウト列を表示します。リストの設定方法については、[詳細なドキュメント](../../platform/using/adobe-campaign-workspace.md#configuring-lists)を参照してください。

   ![](assets/privacy-ccpa-6.png)

1. 列をクリックすると、オプトアウト情報に従って受信者を並べ替えることができます。オプトアウトした受信者のみを表示するフィルターを作成することもできます。フィルターの作成について詳しくは、[こちら](../../platform/using/creating-filters.md)を参照してください。

   ![](assets/privacy-ccpa-7.png)
