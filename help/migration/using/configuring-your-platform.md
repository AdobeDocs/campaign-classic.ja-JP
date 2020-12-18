---
solution: Campaign Classic
product: campaign
title: プラットフォームの設定
description: プラットフォームの設定
audience: migration
content-type: reference
topic-tags: migration-procedure
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 2%

---


# プラットフォームの設定{#configuring-your-platform}

Adobe Campaignv7の一部の主な変更では、有効な動作を確保するための設定が必要です。 これらのパラメーターは、移行の前または後に必要になる場合があります。 この節では、関連する変更とその設定モードについて説明します。

移行中に、**NmsRecipient**&#x200B;テーブルがスキーマ定義から再構築されます。 Adobe Campaign以外でこのテーブルのSQL構造に対して行われた変更は失われます。

チェックする要素の例：

* **NmsRecipient**&#x200B;テーブルに列（またはインデックス）を追加したが、スキーマに詳細を入力していない場合、これは保存されません。
* **tablespace**&#x200B;属性は、デフォルトで値を取り戻します。つまり、デプロイメント・ウィザードで定義された値です。
* NmsRecipientテーブルに参照表示を追加した場合は、移行前にそれを削除する必要があります。

この警告は、Oracleのユーザーにも関係しています。アップグレード後に&#x200B;**usetimestamptz:1**&#x200B;オプションを追加した場合（[タイムゾーン](../../migration/using/general-configurations.md#time-zones)を参照）、少なくとも1つの&#x200B;**date+time**&#x200B;フィールドを含むすべてのテーブルが再構築されます。

## 移行前{#before-the-migration}

Adobe Campaignv7に移行する際は、次の要素を設定する必要があります。 これらの要素は、**アップグレード後**&#x200B;を開始する前にアドレス指定する必要があります。

* タイムゾーン

   v5.11プラットフォームからの移行中に、アップグレード後に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用したい場合は、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

   データベースとしてOracleを使用する場合は、Oracleタイムゾーンファイルがアプリケーションサーバーとデータベースサーバーの間で正しく同期されていることを確認してください。 詳しくは、[Oracle](../../migration/using/general-configurations.md#oracle)の節を参照してください。

* セキュリティゾーン

   セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを構成する必要があります。この場合、移行の前にユーザーIPアドレスを収集する必要があります。

   詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)の節を参照してください。

* 構文

   JavaScriptの一部の構文は、バージョン5.11および6.02では受け入れられる場合があり、新しいインタプリタが使用されるためv7バージョンでは受け入れられなくなります。 詳しくは、[JavaScript](../../migration/using/general-configurations.md#javascript)の節を参照してください。

   同様に、Adobe Campaignv7では、SQLDataベースの構文を置き換える新しい構文が導入されています。 この構文でコード要素を使用する場合は、それらを適合させる必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)の節を参照してください。

* パスワード

   **管理者**&#x200B;と&#x200B;**内部**&#x200B;のパスワードを設定する必要があります。 詳しくは、[ユーザーパスワード](../../migration/using/before-starting-migration.md#user-passwords)の節を参照してください。

* ツリー構造

   v5.11プラットフォームから移行する場合は、Adobe Campaignv6の規則に従ってツリー構造フォルダーを再構成する必要があります。 詳しくは、[Adobe Campaignv7ツリー構造](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure)の節を参照してください。

* インタラクション

   **インタラクション**&#x200B;を使用する場合は、v7に存在しなくなった6.02スキーマ参照をすべて削除する必要があります。 詳しくは、[対話](../../migration/using/general-configurations.md#interaction)の節を参照してください。

## 移行後{#after-the-migration}

**postupgrade**&#x200B;を実行した後、次の要素を考慮し、対応する設定を実行する必要があります。

* ミラーページ

   ミラーページパーソナライゼーションブロックがv6.xで変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージでv5パーソナライゼーションブロックを使用した場合、ミラーページの表示は失敗します。 Adobeでは、メッセージにミラーページを挿入する際に、新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   しかし、一時的な解決策として(そしてミラーページがまだ生きているので)、古いパーソナライゼーションブロックに戻して、**[!UICONTROL XtkAcceptOldPasswords]**&#x200B;を変更し、**[!UICONTROL 1]**&#x200B;に設定すれば、この問題を回避できます。 これは、新しいv6.xパーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関連するエラーが発生した場合は、アップグレード後に、**serverConf.xml**&#x200B;ファイルの&#x200B;**allowSQLInjection**&#x200B;オプションを一時的に有効にする必要があります。これにより、コードを書き直す時間が得られます。 コードの修正後は、必ずセキュリティを再アクティブ化してください。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)を参照してください。

* 競合

   移行はアップグレード後に実行され、レポート、フォーム、Webアプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

   「[競合](../../migration/using/general-configurations.md#conflicts)」の節を参照してください。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳細は、[Tomcat](../../migration/using/general-configurations.md#tomcat)の節を参照してください。

* レポート

   すべての既製のレポートは、現在v6.xレンダリングエンジンを使用しています。 レポートにJavaScriptコードを追加した場合は、一部の要素が変更される可能性があります。

   [「レポート](../../migration/using/general-configurations.md#reports)」セクションを参照してください。

* Web アプリケーション

   アップグレード後、特定のWeb アプリケーションへの接続に問題が発生した場合は、**serverConf.xml**&#x200B;ファイルの&#x200B;**allowUserPassword**&#x200B;オプションと&#x200B;**sessionTokenOnly**&#x200B;オプションをアクティブにする必要があります。 これら2つのオプションは必ず非アクティブにしてください。 詳しくは、「[Identified web applications](../../migration/using/general-configurations.md#identified-web-applications)」の節を参照してください。

   Web アプリケーションのタイプと設定に応じて、追加の操作を実行して正しく動作することを確認する必要があります。

   「[Web アプリケーション](../../migration/using/general-configurations.md#web-applications)」の節を参照してください。

   v5.11プラットフォームから移行する場合は、次の追加設定を行う必要があります。詳しくは、「[Web アプリケーション](../../migration/using/specific-configurations-in-v5-11.md#web-applications)」を参照してください。

* セキュリティゾーン。

   サーバーを起動する前に、セキュリティゾーンを構成する必要があります。 詳しくは、[このセクション](../../installation/using/configuring-campaign-server.md#defining-security-zones)と[セキュリティ](../../migration/using/general-configurations.md#security)を参照してください。

* スキーマ

   Red Hatでは、特定のスキーマの編集時にエラーが発生する場合があります。 詳しくは、[Red-Hat](../../migration/using/general-configurations.md#red-hat)の節を参照してください。

* ワークフロー

   v5.11プラットフォームから移行する場合は、ワークフローランタイムディレクトリを制御する必要があります。 詳しくは、[ワークフロー](../../migration/using/specific-configurations-in-v5-11.md#workflows)の節を参照してください。

* トラッキング

   v5.11プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 詳しくは、「[追跡](../../migration/using/specific-configurations-in-v5-11.md#tracking)」の節を参照してください。

* ホームページ

   v6.02プラットフォームから移行する場合、v6.02から古いホームページを保持するための追加のパラメーターを定義できます。詳細については、[使いやすい情報を参照してください。ホームページとナビゲーション](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation)セクション。

* インタラクション

   **対話処理**&#x200B;を使用する場合は、移行後にパラメーターを調整する必要があります。 詳しくは、[対話](../../migration/using/general-configurations.md#interaction)の節を参照してください。

