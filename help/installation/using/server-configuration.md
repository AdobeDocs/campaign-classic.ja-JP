---
solution: Campaign Classic
product: campaign
title: サーバー設定
description: サーバー設定のベストプラクティスの詳細を表示します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: e1aff73a-54fb-444e-b183-df11c9b3df31
translation-type: tm+mt
source-git-commit: e31d386af4def80cdf258457fc74205b1ca823b3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 73%

---

# サーバー設定 {#server-configuration}

## ファイルアップロードの保護

nlclient／Web インターフェイスを使用して、サーバーにどのようなファイルをアップロードしているかをオペレーターにチェックします。次に、業務上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。詳しくは、[このページ](../../installation/using/configuring-campaign-server.md#limiting-uploadable-files)を参照してください。

Adobe Campaign では、ファイルサイズは制限されません。ただし、IIS/Apacheを設定することで実行できます。 詳しくは、[この節](../../installation/using/web-server-configuration.md)を参照してください。

## リレー

詳細は、[このページ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays)を参照してください。

デフォルトでは、すべての動的ページは、Web モジュールが起動されるマシンのローカルの Tomcat サーバーに自動的にリレーされます。それらの一部をリレーしないように設定することもできます。Adobe Campaign モジュールの一部（Web アプリ、インタラクション、一部の JSP など）を使用しない場合、リレールールから除外できます。

デフォルトでは、HTTP を使用（httpAllowed=&quot;true&quot;）するエンドユーザーリソースを表示するために、この機能を強制的に使用しています。これらのページには、一部の PII（E メールコンテンツ／アドレス）、クーポン、オファーが表示されるので、これらのパスでもう一度 HTTPS を強制する必要があります。

複数のホスト名（公開ホスト名とオペレーター用ホスト名）を使用している場合、オペレーターが必要とするリソースが公開 DNS 名経由でリレーされないようにすることができます。

## 発信接続の保護

Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、が制限される。 新しいURLを許可するには、管理者は[serverConf.xmlファイル](../../installation/using/the-server-configuration-file.md)でURLを参照する必要があります。

3 つの接続保護モードがあります。

* **ブロック** :許可リストに属していないURLはすべてブロックされ、エラーメッセージが表示されます。これは、ポストアップグレード後のデフォルトのモードです。
* **権限設定** :許可リストに属していないURLはすべて許可されます。
* **警告** :許可リスト上にないすべてのURLは許可されますが、JSインタプリタは警告を発し、管理者がそれらを収集できるようにします。このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

新しいクライアントはブロックモードを使用します。新しい URL の許可を希望する場合は、管理者に問い合わせて、その URL を許可リストに追加する必要があります。

移行してきた既存の顧客は、しばらくの間は、警告モードを使用できます。その間、URL を分析する前に、アウトバウンドトラフィックを分析する必要があります。

## コマンドの制限（サーバー側）

いくつかのコマンドがブラックリストに追加され、execCommand 関数で実行できないようになりました。また、セキュリティを強化するために、外部コマンド実行専用の Unix ユーザーが追加されました。ホストされているインスタンスの場合は、この制限が自動的に適用されます。オンプレミスインストールの場合は、[このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)の指示に従って、手動でこの制限を設定できます。 また、ワークフローアクティビティとして「**[!UICONTROL スクリプト]**」と「**[!UICONTROL 外部タスク]**」を選択できなくなりました（新しくインストールされたインスタンスの場合）。

## その他の設定

すべてのページにHTTPヘッダを追加できます（詳しくは、[このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)を参照）。

* HSTS、X-FRAME-OPTIONS、CSP などのヘッダーを追加できます。
* 本番環境に適用する前に、テスト環境でテストする必要があります。

   >[!IMPORTANT]
   >
   >特定のヘッダーを追加すると、Adobe Campaign で異常が発生する場合があります。

Adobe Campaignを使用すると、`<dbcnx .../>`要素にプレーンパスワードを設定できます。 この機能は使用しないでください。

デフォルトでは、Adobe Campaign はセッションを特定の IP に関連付けませんが、この機能を有効にして、セッションが乗っ取られないようにすることができます。これを行うには、[serverConf.xmlファイル](../../installation/using/the-server-configuration-file.md)で、`<authentication>`ノードのcheckIPConsistent属性を&#x200B;**true**&#x200B;に設定します。

デフォルトでは、Adobe Campaign の MTA は、コンテンツを SMTP サーバーに送信する際にセキュリティ保護された接続を使用しません。この機能を有効にする必要があります（配信速度が低下する可能性があります）。これを行うには、`<smtp ...>`ノードで&#x200B;**enableTLS**&#x200B;を&#x200B;**true**&#x200B;に設定します。

認証ノードでセッションの持続時間を短くすることができます（sessionTimeOutSec 属性）。
