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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 2%

---


# プラットフォームの設定{#configuring-your-platform}

Adobe Campaignv7の一部の主な変更では、有効な動作を確保するための設定が必要です。 これらのパラメーターは、移行の前または後に必要になる場合があります。 この節では、関連する変更とその設定モードについて説明します。

移行中に、 **NmsRecipient** テーブルがスキーマ定義から再構築されます。 Adobe Campaign以外でこのテーブルのSQL構造に対して行われた変更は失われます。

チェックする要素の例：

* NmsRecipient **** テーブルに列（またはインデックス）を追加したが、スキーマに詳細を入力していない場合は、この操作は保存されません。
* デフォルトでは、 **tablespace** 属性の値（デプロイメント・ウィザードで定義された値）が戻されます。
* NmsRecipientテーブルに参照表示を追加した場合は、移行前にそれを削除する必要があります。

この警告は、Oracleユーザーにも関係します。アップグレード後に **usetimestamptz:1** オプションを追加した場合( [タイムゾーンを参照](../../migration/using/general-configurations.md#time-zones))は、少なくとも1つの **date+time** フィールドを含むすべてのテーブルが再構築されます。

## 移行前 {#before-the-migration}

Adobe Campaignv7に移行する際は、次の要素を設定する必要があります。 これらの要素は、アップグレード **後に開始する前に指定する必要があります**。

* タイムゾーン

   v5.11プラットフォームからの移行中に、アップグレード後に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) (Time zones)の節を参照してください。

   Oracleをデータベースとして使用する場合は、Oracleタイムゾーン・ファイルがアプリケーション・サーバーとデータベース・サーバーの間で正しく同期されていることを確認します。 For more on this, refer to the [Oracle](../../migration/using/general-configurations.md#oracle) section.

* セキュリティゾーン

   セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを構成する必要があります。この場合、移行の前にユーザーIPアドレスを収集する必要があります。

   For more information, refer to the [Security](../../migration/using/general-configurations.md#security) section.

* 構文

   JavaScriptの一部の構文は、バージョン5.11および6.02では受け入れられる場合があり、新しいインタプリタが使用されるためv7バージョンでは受け入れられなくなります。 For more information, refer to the [JavaScript](../../migration/using/general-configurations.md#javascript) section.

   同様に、Adobe Campaignv7では、SQLDataベースの構文を置き換える新しい構文が導入されています。 この構文でコード要素を使用する場合は、それらを適合させる必要があります。 For more information, refer to the [SQLData](../../migration/using/general-configurations.md#sqldata) section.

* パスワード

   管理者 **パスワードと** 内部 **** パスワードを設定する必要があります。 For more information, refer to the [User passwords](../../migration/using/before-starting-migration.md#user-passwords) section.

* ツリー構造

   v5.11プラットフォームから移行する場合は、Adobe Campaignv6の規則に従ってツリー構造フォルダーを再構成する必要があります。 詳しくは、「 [Adobe Campaignv7ツリー構造](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure) 」の節を参照してください。

* インタラクション

   イン **タラクションを使用する場合**、v7に存在しなくなった6.02スキーマ参照をすべて削除する必要があります。 For more information, refer to the [Interaction](../../migration/using/general-configurations.md#interaction) section.

## 移行後 {#after-the-migration}

アップグレード **後の実行後**、次の要素を考慮し、対応する設定を実行する必要があります。

* ミラーページ

   ミラーページパーソナライゼーションブロックがv6.xで変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージでv5パーソナライゼーションブロックを使用した場合、ミラーページの表示は失敗します。 Adobeでは、メッセージにミラーページを挿入する際に、新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的な解決策として(そしてミラーページがまだ生きているので)、古いパーソナライゼーションブロックに戻して、XtkAcceptOldPasswords **[!UICONTROL を変更し]** 、これを **[!UICONTROL 1に設定すればこの問題を回避できます]**。 これは、新しいv6.xパーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関連するエラーが発生した場合は、アップグレード後に、 **serverConf.xml** ファイルでallowSQLInjection **** オプションを一時的に有効にする必要があります。これにより、コードの書き直しに時間がかかります。 コードの修正後は、必ずセキュリティを再アクティブ化してください。 For more on this, refer to the [SQLData](../../migration/using/general-configurations.md#sqldata) section.

* 競合

   移行はアップグレード後に実行され、レポート、フォーム、Webアプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

   「 [競合](../../migration/using/general-configurations.md#conflicts) 」の節を参照してください。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳細は、「 [Tomcat](../../migration/using/general-configurations.md#tomcat) 」の項を参照してください。

* レポート

   すべての既製のレポートは、現在v6.xレンダリングエンジンを使用しています。 レポートにJavaScriptコードを追加した場合は、一部の要素が変更される可能性があります。

   「 [レポート](../../migration/using/general-configurations.md#reports) 」セクションを参照してください。

* Web アプリケーション

   アップグレード後に、特定のWeb アプリケーションへの接続に問題が発生した場合は、 **serverConf.xml** ファイルで、allowUserPassword **および** sessionTokenOnly **** オプションをアクティブにする必要があります。 これら2つのオプションは必ず非アクティブにしてください。 詳しくは、「 [Identified web applications](../../migration/using/general-configurations.md#identified-web-applications) 」の節を参照してください。

   Web アプリケーションのタイプと設定に応じて、追加の操作を実行して正しく動作することを確認する必要があります。

   「 [Web アプリケーション](../../migration/using/general-configurations.md#web-applications) 」の節を参照してください。

   v5.11プラットフォームから移行する場合は、次の追加設定を行う必要があります。詳しくは、「 [Web アプリケーション](../../migration/using/specific-configurations-in-v5-11.md#web-applications) 」を参照してください。

* セキュリティゾーン。

   サーバーを起動する前に、セキュリティゾーンを構成する必要があります。 詳細については、 [この節](../../installation/using/configuring-campaign-server.md#defining-security-zones) および「 [セキュリティ](../../migration/using/general-configurations.md#security) 」の節を参照してください。

* スキーマ

   Red Hatでは、特定のスキーマの編集時にエラーが発生する場合があります。 For more on this, refer to the [Red-Hat](../../migration/using/general-configurations.md#red-hat) section.

* ワークフロー

   v5.11プラットフォームから移行する場合は、ワークフローランタイムディレクトリを制御する必要があります。 For more on this, refer to the [Workflows](../../migration/using/specific-configurations-in-v5-11.md#workflows) section.

* トラッキング

   v5.11プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 For more on this, refer to the [Tracking](../../migration/using/specific-configurations-in-v5-11.md#tracking) section.

* ホームページ

   v6.02プラットフォームから移行する場合、v6.02から古いホームページを維持するための追加のパラメーターを定義できます。この方法について詳しくは、使いやすい [ユーザーを参照してください。ホームページとナビゲーション](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation) 。

* インタラクション

   イン **タラクションを使用する場合**、移行後にパラメータを調整する必要があります。 For more on this, refer to the [Interaction](../../migration/using/general-configurations.md#interaction) section.

