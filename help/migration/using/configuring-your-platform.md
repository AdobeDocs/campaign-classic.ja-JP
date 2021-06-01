---
product: campaign
title: プラットフォームの設定
description: プラットフォームの設定
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: ad71dead-c0ca-42d5-baa8-0f340979231a
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 2%

---

# プラットフォームの設定{#configuring-your-platform}

Adobe Campaign v7の特定の大きな変更では、有効な操作を確実におこなうために設定が必要です。 これらのパラメーターは、移行の前または後に必要になる場合があります。 この節では、関連する変更とその設定モードについて説明します。

移行中に、**NmsRecipient**&#x200B;テーブルがスキーマ定義から再構築されます。 このテーブルのSQL構造に対してAdobe Campaign以外で行われた変更は失われます。

チェックする要素の例：

* **NmsRecipient**&#x200B;テーブルに列（またはインデックス）を追加したが、スキーマで詳細を指定していない場合、これは保存されません。
* **tablespace**&#x200B;属性は、デフォルトで、デプロイウィザードで定義された値を取り戻します。
* NmsRecipientテーブルに参照ビューを追加した場合は、移行前に削除する必要があります。

この警告は、Oracleユーザーにも関係します。ポストアップグレード中に&#x200B;**usetimestamptz:1**&#x200B;オプションを追加した場合（[タイムゾーン](../../migration/using/general-configurations.md#time-zones)を参照）、少なくとも1つの&#x200B;**date+time**&#x200B;フィールドを含むすべてのテーブルが再構築されます。

## 移行前{#before-the-migration}

Adobe Campaign v7に移行する際に、次の要素を設定する必要があります。 **ポストアップグレード**&#x200B;を開始する前に、これらの要素を指定する必要があります。

* タイムゾーン

   v5.11プラットフォームからの移行中に、ポストアップグレード時に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

   データベースとしてOracleを使用する場合は、アプリケーションサーバーとデータベースサーバーの間でOracleタイムゾーンファイルが正しく同期されていることを確認します。 詳しくは、[Oracle](../../migration/using/general-configurations.md#oracle)の節を参照してください。

* セキュリティゾーン

   セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを設定する必要があります。この場合は、移行前にユーザーIPアドレスを収集する必要があります。

   詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)の節を参照してください。

* 構文

   JavaScriptの特定の構文は、バージョン5.11および6.02で受け入れられ、新しいインタプリタが使用されるので、v7バージョンでは受け入れられなくなる場合があります。 詳しくは、[JavaScript](../../migration/using/general-configurations.md#javascript)の節を参照してください。

   同様に、Adobe Campaign v7では、SQLDataベースの構文を置き換える新しい構文が導入されました。 この構文でコード要素を使用する場合は、コード要素を適応させる必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)の節を参照してください。

* パスワード

   **Admin**&#x200B;および&#x200B;**Internal**&#x200B;パスワードを設定する必要があります。 詳しくは、[ユーザーパスワード](../../migration/using/before-starting-migration.md#user-passwords)の節を参照してください。

* ツリー構造

   v5.11プラットフォームから移行する場合は、Adobe Campaign v6の規則に従ってツリー構造フォルダーを再編成する必要があります。 詳しくは、[Adobe Campaign v7ツリー構造](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure)の節を参照してください。

* インタラクション

   **インタラクション**&#x200B;を使用する場合、v7に存在しなくなった6.02スキーマ参照をすべて削除する必要があります。 詳しくは、[インタラクション](../../migration/using/general-configurations.md#interaction)の節を参照してください。

## 移行後{#after-the-migration}

**postupgrade**&#x200B;を実行した後、次の要素を考慮し、対応する設定を実行する必要があります。

* ミラーページ

   ミラーページのパーソナライゼーションブロックがv6.xで変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージでv5パーソナライゼーションブロックを使用した場合、ミラーページの表示が失敗します。 Adobeでは、メッセージにミラーページを挿入する際に新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的なソリューションとして（ミラーページがまだライブ状態のまま）、古いパーソナライゼーションブロックに戻すと、オプション&#x200B;**[!UICONTROL XtkAcceptOldPasswords]**&#x200B;を変更し、**[!UICONTROL 1]**&#x200B;に設定して、この問題を回避できます。 これは、新しいv6.xパーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関連するエラーが発生した場合は、アップグレード後に、**serverConf.xml**&#x200B;ファイルの&#x200B;**allowSQLInjection**&#x200B;オプションを一時的に有効にする必要があります。これにより、コードを書き換える時間が得られます。 コードを変更したら、必ずセキュリティを再アクティブ化してください。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)の節を参照してください。

* 競合

   移行はポストアップグレードを通じて実行され、レポート、フォーム、Webアプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

   「[競合](../../migration/using/general-configurations.md#conflicts)」の節を参照してください。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳しくは、 [Tomcat](../../migration/using/general-configurations.md#tomcat)の節を参照してください。

* レポート

   すべての標準レポートは、現在v6.xレンダリングエンジンを使用しています。 レポートにJavaScriptコードを追加していた場合は、一部の要素が変更される可能性があります。

   [レポート](../../migration/using/general-configurations.md#reports)の節を参照してください。

* Web アプリケーション

   アップグレード後に、識別されたWebアプリケーションへの接続で問題が発生した場合は、**serverConf.xml**&#x200B;ファイルの&#x200B;**allowUserPassword**&#x200B;および&#x200B;**sessionTokenOnly**&#x200B;オプションを有効にする必要があります。 これらの2つのオプションは、必ず無効にしてください。 詳しくは、[識別されたWebアプリケーション](../../migration/using/general-configurations.md#identified-web-applications)の節を参照してください。

   Webアプリケーションのタイプと設定に応じて、追加の操作を実行して、正しく機能するようにする必要があります。

   [Webアプリケーション](../../migration/using/general-configurations.md#web-applications)の節を参照してください。

   v5.11プラットフォームから移行する場合は、次の追加設定を実行する必要があります。詳しくは、[Webアプリケーション](../../migration/using/specific-configurations-in-v5-11.md#web-applications)の節を参照してください。

* セキュリティゾーン。

   サーバーを起動する前に、セキュリティゾーンを設定する必要があります。 詳しくは、[この節](../../installation/using/security-zones.md)と[セキュリティ](../../migration/using/general-configurations.md#security)の節を参照してください。

* スキーマ

   Red Hatでは、特定のスキーマの編集時にエラーが発生する場合があります。 詳しくは、[Red-Hat](../../migration/using/general-configurations.md#red-hat)の節を参照してください。

* ワークフロー

   v5.11プラットフォームから移行する場合は、ワークフローランタイムディレクトリを制御する必要があります。 詳しくは、[ワークフロー](../../migration/using/specific-configurations-in-v5-11.md#workflows)の節を参照してください。

* トラッキング

   バージョン5.11プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 詳しくは、[トラッキング](../../migration/using/specific-configurations-in-v5-11.md#tracking)の節を参照してください。

* ホームページ

   v6.02プラットフォームから移行する場合は、v6.02から古いホームページを維持するための追加のパラメーターを定義できます。詳しくは、[使いやすさを参照してください。ホームページとナビゲーション](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation)セクション。

* インタラクション

   **インタラクション**&#x200B;を使用する場合は、移行後に任意のパラメーターを調整する必要があります。 詳しくは、[インタラクション](../../migration/using/general-configurations.md#interaction)の節を参照してください。
