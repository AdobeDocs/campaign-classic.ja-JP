---
product: campaign
title: サーバーセキュリティ設定
description: サーバー設定のベストプラクティスについて詳しく見る
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: e1aff73a-54fb-444e-b183-df11c9b3df31
TQID: https://experienceleague.adobe.com/geVW1WFvlnZJmiLeaI01ww-TsQvEN3-zpr57jmz2Miw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 633
ht-degree: 36%

---

# サーバーのセキュリティ設定 {#server-configuration}

## ファイルアップロードの保護

Campaign クライアントコンソールまたはweb インターフェイスを使用して、サーバーにアップロードするファイルの種類を操作ユーザーに確認します。 次に、ビジネス上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。 詳しくは、[このページ](../../installation/using/file-res-management.md)を参照してください。

Adobe Campaignでは、ファイルサイズは制限されません。 IIS/Apacheを設定することで可能です。 詳しくは、[こちら](../../installation/using/web-server-configuration.md)を参照してください。

## リレー

詳しくは、[このページ ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays)を参照してください。

デフォルトでは、すべての動的ページは、Web モジュールが起動されたマシンのローカル Tomcat サーバーに自動的にリレーされます。 それらのいくつかを中継しないことを選択できます。 Adobe Campaign モジュールの一部（Web アプリ、インタラクション、一部の JSP など）を使用しない場合、リレールールから除外できます。

デフォルトでは、http （httpAllowed=&quot;true&quot;）を使用してエンドユーザーリソースを表示する機能を強制しました。 これらのページには、一部の PII（E メールコンテンツ／アドレス）、クーポン、オファーが表示されるので、これらのパスでもう一度 HTTPS を強制する必要があります。

複数のホスト名（公開ホスト名とオペレーター用ホスト名）を使用している場合、オペレーターが必要とするリソースが公開 DNS 名経由でリレーされないようにすることができます。

## 送信接続の保護

JavaScript コードで呼び出すことができるURLのデフォルトリスト（ワークフローなど） 限定的なものです。 新しいURLを許可するには、管理者が[serverConf.xml ファイル ](../../installation/using/the-server-configuration-file.md)でURLを参照する必要があります。

3 つの接続保護モードがあります。

* **ブロッキング** :「」許可リストに属しないすべてのURLがブロックされ、エラーメッセージが表示されます。 これは、ポストアップグレード後のデフォルトのモードです。
* **Permissive**：この許可リストに属しないすべてのURLが許可されます。
* **Warning** :Administratorが警告を収集できるように、許可リストにないURLはすべて許可されますが、JS インタープリターは警告を発します。 このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

新しいクライアントはブロッキングモードを使用します。 新しいURLを許可する場合は、管理者に連絡してURLを管理者許可リストに追加する必要があります。

移行を行う既存のお客様は、しばらくの間、警告モードを使用できます。 また、URLを承認する前に、アウトバウンドトラフィックを分析する必要があります。

## コマンドの制限（サーバー側）

ExeccCommand関数を使用して実行することはできません。このコマンドはのブロックリストに含まれています。 外部コマンドを実行する専用のUnix ユーザーは、セキュリティを強化します。 ホスト型インストールの場合、この制限は自動的に適用されます。 オンプレミス インストールの場合は、[このページ ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)の指示に従って、この制限を手動で設定できます。 また、ワークフローアクティビティとして「**[!UICONTROL スクリプト]**」と「**[!UICONTROL 外部タスク]**」を選択できなくなりました（新しくインストールされたインスタンスの場合）。

## その他の設定

すべてのページに追加のHTTP ヘッダーを追加できます（詳細については、[このページ ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)を参照）。

* HSTS、X-FRAME-OPTIONS、CSP などのヘッダーを追加できます。
* 本番環境に適用する前に、テスト環境でテストする必要があります。

  >[!IMPORTANT]
  >
  >特定のヘッダーを追加すると、Adobe Campaign で異常が発生する場合があります。

Adobe Campaignでは、`<dbcnx .../>`要素にプレーンパスワードを設定できます。 この機能は使用しないでください。

デフォルトでは、Adobe Campaignはセッションを特定のIPに固定しませんが、セッションが盗まれるのを防ぐためにセッションをアクティブにすることができます。 これを行うには、[serverConf.xml ファイル ](../../installation/using/the-server-configuration-file.md)で、`<authentication>` ノードのcheckIPConsistent属性を&#x200B;**true**&#x200B;に設定します。

デフォルトでは、Adobe CampaignのMTAは、セキュアな接続を使用してコンテンツをSMTP サーバーに送信しません。 この機能を有効にする必要があります（配信速度が遅くなる可能性があります）。 これを行うには、`<smtp ...>` ノードの&#x200B;**enableTLS**&#x200B;を&#x200B;**true**&#x200B;に設定します。

認証ノードでセッションの持続時間を短くすることができます（sessionTimeOutSec 属性）。
