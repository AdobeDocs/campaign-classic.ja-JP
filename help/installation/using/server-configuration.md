---
product: campaign
title: サーバーのセキュリティ設定
description: サーバー設定のベストプラクティスの詳細を説明します
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: e1aff73a-54fb-444e-b183-df11c9b3df31
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 39%

---

# サーバーのセキュリティ設定 {#server-configuration}

## ファイルアップロードの保護

Campaign クライアントコンソールまたは Web インターフェイスを使用して、サーバーにアップロードするファイルの種類をオペレーショナルユーザーに確認します。 次に、ビジネス上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。詳しくは、[このページ](../../installation/using/file-res-management.md)を参照してください。

Adobe Campaignでは、ファイルサイズは制限されません。 ただし、IIS/Apache を設定することで実行できます。 詳しくは、[こちら](../../installation/using/web-server-configuration.md)を参照してください。

## リレー

詳しくは、 [このページ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) を参照してください。

デフォルトでは、すべての動的ページは、Web モジュールが起動されたマシンのローカル Tomcat サーバーに自動的にリレーされます。 一部をリレーしないように選択できます。 Adobe Campaign モジュールの一部（Web アプリ、インタラクション、一部の JSP など）を使用しない場合、リレールールから除外できます。

初期設定では、http (httpAllowed=&quot;true&quot;) を使用してエンドユーザーリソースを表示する機能が強制されました。 これらのページには、一部の PII（E メールコンテンツ／アドレス）、クーポン、オファーが表示されるので、これらのパスでもう一度 HTTPS を強制する必要があります。

複数のホスト名（公開ホスト名とオペレーター用ホスト名）を使用している場合、オペレーターが必要とするリソースが公開 DNS 名経由でリレーされないようにすることができます。

## 送信接続の保護

Campaign のインスタンスが JavaScript コード（ワークフローなど）で呼び出せる URL のデフォルトリストはは制限されています。 新しい URL を許可するには、管理者が [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md).

3 つの接続保護モードがあります。

* **ブロック** ：特定のに属さないすべての URL がブ許可リストに加えるロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **許容** ：特定の URL に属さないすべての URL を許許可リストに加える可します。
* **警告** ：上にない URL はすべて許可されま許可リストに加えるすが、JS インタープリターから警告が表示されるので、管理者がそれらを収集できます。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

新しいクライアントはブロックモードを使用します。 新しい URL を許可する場合は、管理者に問い合わせて、URL を管理者に追加する必要があり許可リストに加えるます。

移行による既存のお客様は、しばらくの間、警告モードを使用できます。 その間、URL を認証する前に、送信トラフィックを分析する必要があります。

## コマンドの制限（サーバー側）

複数のコマンドがに含まブロックリストに加えるれており、 execCommand 関数を使用して実行することはできません。 外部コマンドを実行する専用の Unix ユーザーがセキュリティを強化します。 ホストインストールの場合、この制限は自動的に適用されます。 オンプレミスインストールの場合は、次の手順に従って、この制限を手動で設定できます。 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands). また、ワークフローアクティビティとして「**[!UICONTROL スクリプト]**」と「**[!UICONTROL 外部タスク]**」を選択できなくなりました（新しくインストールされたインスタンスの場合）。

## その他の設定

すべてのページに HTTP ヘッダーを追加できます ( 詳しくは、 [このページ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)):

* HSTS、X-FRAME-OPTIONS、CSP などのヘッダーを追加できます。
* 本番環境に適用する前に、テスト環境でテストする必要があります。

  >[!IMPORTANT]
  >
  >特定のヘッダーを追加すると、Adobe Campaign で異常が発生する場合があります。

Adobe Campaignを使用すると、 `<dbcnx .../>` 要素を選択します。 この機能は使用しないでください。

デフォルトでは、Adobe Campaignはセッションを特定の IP に固定しませんが、この機能を有効にして、セッションが盗難にあうのを防ぐことができます。 これをおこなうには、「 [serverConf.xml ファイル](../../installation/using/the-server-configuration-file.md)に設定し、checkIPConsistent 属性をに設定します。 **true** （内） `<authentication>` ノード。

デフォルトでは、Adobe Campaignの MTA は、SMTP サーバーにコンテンツを送信する際に、セキュリティで保護された接続を使用しません。 この機能を有効にする必要があります（配信速度が遅くなる場合があります）。 これをおこなうには、 **enableTLS** から **true** （内） `<smtp ...>` ノード。

認証ノードでセッションの持続時間を短くすることができます（sessionTimeOutSec 属性）。
