---
product: campaign
title: サーバーのセキュリティ設定
description: サーバー設定のベストプラクティスの詳細を説明します
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: e1aff73a-54fb-444e-b183-df11c9b3df31
source-git-commit: e55fff99fd5dec8da998310dc7026c1a506abadc
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 62%

---

# サーバーのセキュリティ設定 {#server-configuration}

![](../../assets/v7-only.svg)

## ファイルアップロードの保護

Campaign クライアントコンソールまたは Web インターフェイスを使用して、サーバーにアップロードするファイルの種類をオペレーショナルユーザーに確認します。 次に、ビジネス上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。詳しくは、[このページ](../../installation/using/file-res-management.md)を参照してください。

Adobe Campaign では、ファイルサイズは制限されません。ただし、IIS/Apache を設定することで実行できます。 詳しくは、[この節](../../installation/using/web-server-configuration.md)を参照してください。

## リレー

詳しくは、 [このページ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) を参照してください。

デフォルトでは、すべての動的ページは、Web モジュールが起動されるマシンのローカルの Tomcat サーバーに自動的にリレーされます。それらの一部をリレーしないように設定することもできます。Adobe Campaign モジュールの一部（Web アプリ、インタラクション、一部の JSP など）を使用しない場合、リレールールから除外できます。

デフォルトでは、HTTP を使用（httpAllowed=&quot;true&quot;）するエンドユーザーリソースを表示するために、この機能を強制的に使用しています。これらのページには、一部の PII（E メールコンテンツ／アドレス）、クーポン、オファーが表示されるので、これらのパスでもう一度 HTTPS を強制する必要があります。

複数のホスト名（公開ホスト名とオペレーター用ホスト名）を使用している場合、オペレーターが必要とするリソースが公開 DNS 名経由でリレーされないようにすることができます。

## 発信接続の保護

Campaign のインスタンスが JavaScript コード（ワークフローなど）で呼び出せる URL のデフォルトリストはは制限されています。 新しい URL を許可するには、管理者が [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md).

3 つの接続保護モードがあります。

* **ブロック** :そのページに属さないすべての URL がブ許可リストロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容** :このタブに属さないすべての URL が許許可リスト可されます。
* **警告** :上にないすべての URL が許可されま許可リストすが、JS インタープリタが警告を表示するので、管理者がそれらを収集できます。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

新しいクライアントはブロックモードを使用します。新しい URL を許可する場合は、管理者に問い合わせて、URL を管理者に追加する必要があり許可リストます。

移行してきた既存の顧客は、しばらくの間は、警告モードを使用できます。その間、URL を認証する前に、送信トラフィックを分析する必要があります。

## コマンドの制限（サーバー側）

複数のコマンドがに含まブロックリストれており、 execCommand 関数を使用して実行することはできません。 また、セキュリティを強化するために、外部コマンド実行専用の Unix ユーザーが追加されました。ホストされているインスタンスの場合は、この制限が自動的に適用されます。オンプレミスインストールの場合は、次の手順に従って、この制限を手動で設定できます。 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands). また、ワークフローアクティビティとして「**[!UICONTROL スクリプト]**」と「**[!UICONTROL 外部タスク]**」を選択できなくなりました（新しくインストールされたインスタンスの場合）。

## その他の設定

すべてのページに HTTP ヘッダーを追加できます ( 詳しくは、 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)):

* HSTS、X-FRAME-OPTIONS、CSP などのヘッダーを追加できます。
* 本番環境に適用する前に、テスト環境でテストする必要があります。

   >[!IMPORTANT]
   >
   >特定のヘッダーを追加すると、Adobe Campaign で異常が発生する場合があります。

Adobe Campaignでは、 `<dbcnx .../>` 要素。 この機能は使用しないでください。

デフォルトでは、Adobe Campaign はセッションを特定の IP に関連付けませんが、この機能を有効にして、セッションが乗っ取られないようにすることができます。これをおこなうには、 [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md)に設定し、checkIPConsistent 属性をに設定します。 **true** 内 `<authentication>` ノード。

デフォルトでは、Adobe Campaign の MTA は、コンテンツを SMTP サーバーに送信する際にセキュリティ保護された接続を使用しません。この機能を有効にする必要があります（配信速度が低下する可能性があります）。これをおこなうには、 **enableTLS** から **true** 内 `<smtp ...>` ノード。

認証ノードでセッションの持続時間を短くすることができます（sessionTimeOutSec 属性）。
