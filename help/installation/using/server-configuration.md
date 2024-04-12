---
product: campaign
title: サーバーのセキュリティ設定
description: サーバー設定のベストプラクティスの詳細を学ぶ
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: e1aff73a-54fb-444e-b183-df11c9b3df31
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 39%

---

# サーバーのセキュリティ設定 {#server-configuration}

## ファイルアップロードの保護

Campaign クライアントコンソールまたは web インターフェイスを使用して、オペレーショナルユーザーがサーバーにアップロードするファイルの種類を確認します。 次に、ビジネス上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。詳しくは、[このページ](../../installation/using/file-res-management.md)を参照してください。

Adobe Campaignでは、ファイルサイズは制限されません。 ただし、IIS/Apache を設定することで実行できます。 詳しくは、[こちら](../../installation/using/web-server-configuration.md)を参照してください。

## リレー

を参照してください。 [このページ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) を参照してください。

デフォルトでは、すべての動的ページは、Web モジュールを起動したマシンのローカル Tomcat サーバーに自動的に中継されます。 一部の機能はリレーしないように選択できます。 Adobe Campaign モジュールの一部（Web アプリ、インタラクション、一部の JSP など）を使用しない場合、リレールールから除外できます。

デフォルトでは、http （httpAllowed=&quot;true&quot;）を使用してエンドユーザーのリソースを強制的に表示するようになりました。 これらのページには、一部の PII（E メールコンテンツ／アドレス）、クーポン、オファーが表示されるので、これらのパスでもう一度 HTTPS を強制する必要があります。

複数のホスト名（公開ホスト名とオペレーター用ホスト名）を使用している場合、オペレーターが必要とするリソースが公開 DNS 名経由でリレーされないようにすることができます。

## 送信接続の保護

Campaign のインスタンスが JavaScript コード（ワークフローなど）で呼び出せる URL のデフォルトリストは制限されています。 新しい URL を許可するには、管理者はで URL を参照する必要があります。 [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md).

3 つの接続保護モードがあります。

* **ブロック** :許可リストに属さないすべての URL はブロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容値** :許可リストに属さないすべての URL が許可されます。
* **警告** :許可リスト上の URL 以外の URL はすべて許可されますが、JS インタープリターは警告を表示して、管理者が URL を収集できるようにします。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

新しいクライアントはブロッキング モードを使用します。 新しい URL を許可する場合は、管理者に連絡して、URL を許可リストに追加してもらう必要があります。

移行を行った既存のお客様は、しばらくの間、警告モードを使用できます。 一方、URL を承認する前に、送信トラフィックを分析する必要があります。

## コマンドの制限（サーバー側）

ブロックリストには複数のコマンドが含まれており、execCommand 関数を使用して実行することはできません。 外部コマンドを実行する専用の Unix ユーザーによって、セキュリティが強化されます。 ホスト環境でのインストールの場合、この制限は自動的に適用されます。 オンプレミスインストールの場合は、の手順に従って、この制限を手動で設定できます。 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands). また、ワークフローアクティビティとして「**[!UICONTROL スクリプト]**」と「**[!UICONTROL 外部タスク]**」を選択できなくなりました（新しくインストールされたインスタンスの場合）。

## その他の設定

すべてのページに追加の HTTP ヘッダーを追加することができます（詳しくは、 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)）:

* HSTS、X-FRAME-OPTIONS、CSP などのヘッダーを追加できます。
* 本番環境に適用する前に、テスト環境でテストする必要があります。

  >[!IMPORTANT]
  >
  >特定のヘッダーを追加すると、Adobe Campaign で異常が発生する場合があります。

Adobe Campaignでは、 `<dbcnx .../>` 要素。 この機能は使用しないでください。

デフォルトでは、Adobe Campaignはセッションを特定の IP に固定しませんが、セッションが盗まれるのを防ぐためにアクティブにすることができます。 これを行うには、 [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md):checkIPConsistent 属性をに設定します **true** が含まれる `<authentication>` ノード。

デフォルトでは、Adobe Campaign MTA はコンテンツを SMTP サーバーに送信する際に、セキュリティで保護された接続を使用しません。 この機能を有効にする必要があります（配信速度が低下する可能性があります）。 それには、を設定します **enableTLS** 対象： **true** が含まれる `<smtp ...>` ノード。

認証ノードでセッションの持続時間を短くすることができます（sessionTimeOutSec 属性）。
