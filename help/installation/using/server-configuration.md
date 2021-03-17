---
solution: Campaign Classic
product: campaign
title: サーバー設定
description: サーバー設定のベストプラクティスの詳細を表示します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: d88815e36f7be1b010dcaeee51013a5da769b4a8
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 77%

---


# サーバー設定 {#server-configuration}

## セキュリティゾーンの設定

>[!IMPORTANT]
>
>8977以降では、セキュリティゾーンのセルフサービスユーザーインターフェイスは使用できなくなりました。
>
>* AWSでホストしている場合は、許可リストにIPを追加するCampaign コントロールパネルを実行する必要があります。 詳しくは、[該当するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html)を参照してください。
>* AWS でホストされていない場合は、アドビのサポートチームに連絡し、IP を許可リストに追加してもらってください。

>
>
インスタンスが AWS でホストされているかどうかを確認するには、[この節](https://experienceleague.adobe.com/docs/control-panel/using/faq.html)に記載されている手順に従います。

* subNetwork でリバースプロキシが許可されていないことを確認します。許可されている場合は、**すべての**&#x200B;トラフィックがこのローカル IP から来ているものとして検出され、信頼されます。

* sessionTokenOnly=&quot;true&quot; の使用は最小限に抑えます。

   * 警告：この属性がtrueに設定されている場合、演算子は&#x200B;**CRSF攻撃**&#x200B;にさらされる可能性があります。
   * さらに、sessionToken cookie に httpOnly フラグが設定されていないので、一部のクライアント側 JavaScript コードがこれを読み取れる可能性があります。
   * ただし、複数の実行セルで Message Center が sessionTokenOnly を必要とします。新しいセキュリティゾーンを作成し、sessionTokenOnly を true に設定して、**必要な IP のみ**&#x200B;をこのゾーンに追加します。

* 可能な場合は、allowHTTPとshowErrorsをすべてfalseに設定し（localhostではなく）、確認します。

   * allowHTTP = &quot;false&quot;：オペレーターは HTTPS を使用することを強制されます。
   * showErrors = &quot;false&quot;：技術的エラー（SQL エラーなど）を非表示にします。これにより、表示される情報の量を抑えられますが、マーケターが（管理者に追加情報を要求することなしに）問題を解決することが難しくなります。

* 調査、webApp、レポートを作成（実際にはプレビュー）する必要があるマーケティングユーザーまたは管理者が使用する IP に対してのみ、allowDebug を true に設定します。このフラグを使用すると、これらの IP でリレールールが表示され、デバッグできるようになります。

* allowEmptyPassword、allowUserPassword、allowSQLInjection は決して true に設定しないでください。これらの属性は、v5 や v6.0 からの移行のためだけにあります。

   * **allowEmptyPassword** を使用すると、オペレーターは空のパスワードを設定できます。この属性を使用する場合、すべてのオペレーターに所定の期限までにパスワードを設定するよう通知してください。この期限を経過したら、この属性を false に設定します。

   * **allowUserPassword** を使用すると、オペレーターは資格情報をパラメーターとして送信できます（この情報は、Apache、IIS、プロキシでログに記録されます）。この機能は、以前に API の使用を簡素化するために使用されていました。クックブック（または仕様）で、サードパーティのアプリケーションがこれを使用していないかをチェックできます。使用されている場合、API の使用方法を変更して、なるべく早くこの機能を削除するよう通知する必要があります。

   * **allowSQLInjection** を使用すると、ユーザーは古い構文を使用した SQL インジェクションを実行できます。[このページ](../../migration/using/general-configurations.md)で説明されている修正をできるだけ早く行い、この属性をfalseに設定できるようにします。 /nl/jsp/ping.jsp?zones=true を使用すると、セキュリティゾーン設定をチェックできます。このページには、現在の IP のセキュリティ対策のアクティブステータス（これらのセキュリティフラグで計算）が表示されます。

* HttpOnly cookie／useSecurityToken：**sessionTokenOnly** フラグを参照してください。

* 許可リストに追加する IP を最小限に抑える：セキュリティゾーンには、既にプライベートネットワーク用の 3 つの範囲が追加されています。通常、これらの IP アドレスをすべて使用することはありません。そのため、必要なもののみを保持するようにしてください。

* webApp／内部オペレーターを更新して、localhost でのみアクセス可能となるようにしてください。

## ファイルアップロードの保護

nlclient／Web インターフェイスを使用して、サーバーにどのようなファイルをアップロードしているかをオペレーターにチェックします。次に、業務上必要である可能性のあるものを示します。

* 画像（jpg、gif、png など）
* コンテンツ（zip、html、css など）
* マーケティングアセット（doc、xls、pdf、psd、tiff など）
* E メール添付ファイル（doc、pdf など）
* ETL（txt、csv、tab など）
* その他

これらすべてを serverConf/shared/datastore/@uploadAllowlist（有効な Java 正規表現）に追加します。詳しくは、[こちらのページ](../../installation/using/configuring-campaign-server.md#limiting-uploadable-files)を参照してください。

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
