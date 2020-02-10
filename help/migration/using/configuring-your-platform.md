---
title: プラットフォームの設定
seo-title: プラットフォームの設定
description: プラットフォームの設定
seo-description: null
page-status-flag: never-activated
uuid: e6255e4b-c9c8-4ac9-9ee3-aaa4dc9e5ecf
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migration-procedure
discoiquuid: 4d2e765b-750b-457f-ad55-8bd6faaa86af
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 34cd6e6cf5652c9e2163848c2b1ef32f53ee6ca4

---


# プラットフォームの設定{#configuring-your-platform}

Adobe Campaign v7の大きな変更の一部は、有効な操作を確実に行うために設定が必要です。 これらのパラメーターは、移行の前後に必要になる場合があります。 この節では、関連する変更とその設定モードについて説明します。

移行中に、NmsRecipientテーブル **が** 、スキーマ定義から再構築されます。 この表のSQL構造に対してAdobe Campaign以外で行われた変更はすべて失われます。

確認する要素の例：

* NmsRecipientテーブルに列（またはインデックス）を追加したが、 **NmsRecipient** テーブルをスキーマに詳細化していない場合、この値は保存されません。
* デフォ **ルトでは** 、tablespace属性の値（デプロイメント・ウィザードで定義された値）が戻されます。
* NmsRecipientテーブルに参照ビューを追加した場合は、移行する前に削除する必要があります。

この警告は、Oracleユーザーにも関係します。アップグレード後に **usetimestamptz:1** オプションを追加した場合( [Time zonesを参照](../../migration/using/general-configurations.md#time-zones))、少なくとも1つの日付+時間フィールドを含むすべてのテ **** ーブルが再構築されます。

## 移行前 {#before-the-migration}

Adobe Campaign v7に移行する際は、次の要素を設定する必要があります。 アップグレード後に開始する前に、これらの要素に対応する必要 **がありま**&#x200B;す。

* タイムゾーン

   v5.11プラットフォームからの移行中に、アップグレード後に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、タイムゾーンの節を参照 [してください](../../migration/using/general-configurations.md#time-zones) 。

   Oracleをデータベースとして使用する場合は、Oracleタイムゾーン・ファイルがアプリケーション・サーバーとデータベース・サーバーの間で正しく同期されていることを確認します。 For more on this, refer to the [Oracle](../../migration/using/general-configurations.md#oracle) section.

   さらに、v.5.11プラットフォームからの移行中に、MySQLで追加の設定を実行する必要があります。 For more information, refer to the [MySQL](../../migration/using/specific-configurations-in-v5-11.md#mysql) section.

* セキュリティゾーン

   セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを設定する必要があります。この場合、移行前にユーザーIPアドレスを収集する必要があります。

   For more information, refer to the [Security](../../migration/using/general-configurations.md#security) section.

* 構文

   JavaScriptの一部の構文は、バージョン5.11および6.02では受け入れられ、新しいインタープリターが使用されるので、v7バージョンでは受け入れられなくなります。 For more information, refer to the [JavaScript](../../migration/using/general-configurations.md#javascript) section.

   同様に、SQLDataベースの構文を置き換える新しい構文がAdobe Campaign v7で導入されました。 この構文でコード要素を使用する場合は、それらを適応させる必要があります。 For more information, refer to the [SQLData](../../migration/using/general-configurations.md#sqldata) section.

* パスワード

   管理者パスワードと内部パスワ **ードを設定す** る必要があります **** 。 For more information, refer to the [User passwords](../../migration/using/before-starting-migration.md#user-passwords) section.

* ツリー構造

   v5.11プラットフォームから移行する場合は、Adobe Campaign v6の規則に従ってツリー構造のフォルダーを再構成する必要があります。 詳しくは、「 [Adobe Campaign v7ツリー構造」の節を参照してください](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure) 。

* インタラクション

   インタラクシ **ョンを使用する場合**、v7に存在しなくなった6.02スキーマ参照をすべて削除する必要があります。 For more information, refer to the [Interaction](../../migration/using/general-configurations.md#interaction) section.

## 移行後 {#after-the-migration}

アップグレード **後の実行後**、次の要素と、対応する設定を考慮する必要があります。

* ミラーページ

   ミラーページのパーソナライゼーションブロックがv6.xで変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージでv5パーソナライゼーションブロックを使用した場合、ミラーページの表示は失敗します。 メッセージにミラーページを挿入する際は、新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的なソリューションとして（ミラーページがまだ生きているので）、古いパーソナライゼーションブロックに戻して、オプションを変更してをに設定することで、この問題を回避す **[!UICONTROL XtkAcceptOldPasswords]** ることができま **[!UICONTROL 1]**&#x200B;す。 これは、新しいv6.xパーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関連するエラーが発生した場合は、アップグレード後に、 **serverConf.xmlファイルで** allowSQLInjection **** オプションを一時的に有効にする必要があります。これにより、コードの書き直しに時間がかかります。 コードを変更したら、必ずセキュリティを再アクティブ化してください。 For more on this, refer to the [SQLData](../../migration/using/general-configurations.md#sqldata) section.

* 競合

   移行はアップグレード後に実行され、競合がレポート、フォーム、Webアプリケーションに表示される場合があります。 これらの競合は、コンソールから解決できます。

   「競合」の節を参 [照してください](../../migration/using/general-configurations.md#conflicts) 。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳細は、「 [Tomcat](../../migration/using/general-configurations.md#tomcat) 」の項を参照してください。

* レポート

   そのまま使用できるすべてのレポートは、現在v6.xレンダリングエンジンを使用しています。 レポートにJavaScriptコードを追加した場合、一部の要素が変更される可能性があります。

   「レポート」セクシ [ョンを参照](../../migration/using/general-configurations.md#reports) 。

* Web アプリケーション

   アップグレード後に、特定したWebアプリケーションへの接続で問題が発生した場合は、 **serverConf.xmlファイルで** allowUserPassword **オプションと** sessionTokenOnly **オプションを有効にする必要があります** 。 この2つのオプションは必ず非アクティブにしてください。 詳しくは、「識別されたWebアプリケーション [」の節を参照してください](../../migration/using/general-configurations.md#identified-web-applications) 。

   Webアプリケーションのタイプと設定に応じて、正しく動作するように追加の操作を実行する必要があります。

   詳しくは、 [Webアプリケーション](../../migration/using/general-configurations.md#web-applications) 「」を参照してください。

   v5.11プラットフォームから移行する場合は、次の追加設定を行う必要があります。詳しくは、「 [Webアプリケーション](../../migration/using/specific-configurations-in-v5-11.md#web-applications) 」を参照してください。

* セキュリティゾーン。

   サーバーを起動する前に、セキュリティゾーンを構成する必要があります。 詳細については、この節と [「セキュリティ](../../installation/using/configuring-campaign-server.md#defining-security-zones) 」を参照 [します](../../migration/using/general-configurations.md#security) 。

* スキーマ

   Red hatでは、特定のスキーマを編集する際にエラーが発生する場合があります。 For more on this, refer to the [Red-Hat](../../migration/using/general-configurations.md#red-hat) section.

* ワークフロー

   v5.11プラットフォームから移行する場合は、workflowsランタイムディレクトリを制御する必要があります。 For more on this, refer to the [Workflows](../../migration/using/specific-configurations-in-v5-11.md#workflows) section.

* トラッキング

   v5.11プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 For more on this, refer to the [Tracking](../../migration/using/specific-configurations-in-v5-11.md#tracking) section.

* ホームページ

   v6.02プラットフォームから移行する場合は、v6.02から古いホームページを維持するための追加のパラメーターを定義できます。詳しくは、「使いやすさ」を参照し [てください。ホームページとナビゲーション](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation) ・セクション。

* インタラクション

   インタラクションを使 **用する場合**、移行後にパラメータを調整する必要があります。 For more on this, refer to the [Interaction](../../migration/using/general-configurations.md#interaction) section.

