---
product: campaign
title: プラットフォームの設定
description: プラットフォームの設定
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: ad71dead-c0ca-42d5-baa8-0f340979231a
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 2%

---

# プラットフォームの設定{#configuring-your-platform}

![](../../assets/v7-only.svg)

Adobe Campaign v7 の大きな変更の一部では、有効な操作を確実におこなうために設定が必要です。 これらのパラメーターは、移行の前または後に必要になる場合があります。 この節では、関連する変更とその設定モードについて説明します。

移行中に、**NmsRecipient** テーブルがスキーマ定義から再構築されます。 このテーブルの SQL 構造に対してAdobe Campaign以外で行われた変更は失われます。

チェックする要素の例：

* **NmsRecipient** テーブルに列（またはインデックス）を追加したが、スキーマで詳細を指定していない場合、この列は保存されません。
* **tablespace** 属性は、デフォルトで、デプロイ・ウィザードで定義された値を取り戻します。
* NmsRecipient テーブルに参照ビューを追加した場合は、移行前に削除する必要があります。

この警告は、Oracleユーザーにも影響します。ポストアップグレード中に **usetimestamptz:1** オプションを追加した場合（[ タイムゾーン ](../../migration/using/general-configurations.md#time-zones) を参照）、少なくとも 1 つの **日付+時刻** フィールドを含むすべてのテーブルが再構築されます。

## 移行前 {#before-the-migration}

Adobe Campaign v7 に移行する場合は、次の要素を設定する必要があります。 **ポストアップグレード** を開始する前に、これらの要素に対処する必要があります。

* タイムゾーン

   v5.11 プラットフォームからの移行中に、ポストアップグレード時に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、[ タイムゾーン ](../../migration/using/general-configurations.md#time-zones) の節を参照してください。

   oracleをデータベースとして使用する場合は、アプリケーションサーバーとOracleサーバーの間でデータベースタイムゾーンファイルが正しく同期されていることを確認します。 詳しくは、[Oracle](../../migration/using/general-configurations.md#oracle) の節を参照してください。

* セキュリティゾーン

   セキュリティ上の理由により、Adobe Campaignプラットフォームは、デフォルトではアクセスできなくなりました。セキュリティゾーンを設定する必要があります。この場合は、移行前にユーザーの IP アドレスを収集する必要があります。

   詳しくは、[ セキュリティ ](../../migration/using/general-configurations.md#security) の節を参照してください。

* 構文

   JavaScript の特定の構文は、バージョン 5.11 および 6.02 で受け入れられ、新しいインタープリターの使用により v7 バージョンでは受け入れられなくなる場合があります。 詳しくは、[JavaScript](../../migration/using/general-configurations.md#javascript) の節を参照してください。

   同様に、SQLData ベースの構文を置き換える新しい構文がAdobe Campaign v7 で導入されました。 この構文でコード要素を使用する場合は、コード要素を適応させる必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

* パスワード

   **Admin** および **Internal** パスワードを設定する必要があります。 詳しくは、[ ユーザーパスワード ](../../migration/using/before-starting-migration.md#user-passwords) の節を参照してください。

* ツリー構造

   v5.11 プラットフォームから移行する場合は、Adobe Campaign v6 の規則に従ってツリー構造フォルダーを再編成する必要があります。 詳しくは、[Adobe Campaign v7 のツリー構造 ](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure) の節を参照してください。

* インタラクション

   **インタラクション** を使用する場合は、v7 に存在しない 6.02 スキーマ参照をすべて削除する必要があります。 詳しくは、[ インタラクション ](../../migration/using/general-configurations.md#interaction) の節を参照してください。

## 移行後 {#after-the-migration}

**postupgrade** を実行した後、次の要素を考慮し、対応する設定を実行する必要があります。

* ミラーページ

   ミラーページのパーソナライゼーションブロックが v6.x で変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージで v5 パーソナライゼーションブロックを使用すると、ミラーページの表示に失敗します。 Adobeでは、メッセージにミラーページを挿入する際に新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的な解決策として（ミラーページがまだ公開されているので）、古いパーソナライゼーションブロックに戻すと、オプション **[!UICONTROL XtkAcceptOldPasswords]** を変更し、**[!UICONTROL 1]** に設定して、この問題を回避できます。 これは、新しい v6.x パーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関連するエラーが発生した場合は、アップグレード後に、**serverConf.xml** ファイルの **allowSQLInjection** オプションを一時的に有効にする必要があります。これにより、コードを書き換える時間が得られます。 コードを変更したら、必ずセキュリティを再アクティブ化してください。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

* 競合

   移行はポストアップグレードを通じて実行され、レポート、フォーム、Web アプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

   [ 競合 ](../../migration/using/general-configurations.md#conflicts) の節を参照してください。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳しくは、[Tomcat](../../migration/using/general-configurations.md#tomcat) の節を参照してください。

* レポート

   すべての標準レポートで、現在 v6.x レンダリングエンジンが使用されています。 レポートに JavaScript コードを追加していた場合は、一部の要素が変更される場合があります。

   [ レポート ](../../migration/using/general-configurations.md#reports) の節を参照してください。

* Web アプリケーション

   アップグレード後に、識別された Web アプリケーションへの接続に問題が発生した場合は、**serverConf.xml** ファイルの **allowUserPassword** および **sessionTokenOnly** オプションを有効にする必要があります。 この 2 つのオプションは、必ず無効にしてください。 詳しくは、[ 識別された Web アプリケーション ](../../migration/using/general-configurations.md#identified-web-applications) の節を参照してください。

   Web アプリケーションのタイプと設定に応じて、追加の操作を実行して、正しく機能するようにする必要があります。

   [Web アプリケーション ](../../migration/using/general-configurations.md#web-applications) の節を参照してください。

   v5.11 プラットフォームから移行する場合は、次の追加設定を実行する必要があります。詳しくは、[Web アプリケーション ](../../migration/using/specific-configurations-in-v5-11.md#web-applications) の節を参照してください。

* セキュリティゾーン.

   サーバーを起動する前に、セキュリティゾーンを設定する必要があります。 詳しくは、[ この節 ](../../installation/using/security-zones.md) と [ セキュリティ ](../../migration/using/general-configurations.md#security) の節を参照してください。

* スキーマ

   Red Hat では、特定のスキーマを編集する際にエラーが発生する場合があります。 詳しくは、[Red-Hat](../../migration/using/general-configurations.md#red-hat) の節を参照してください。

* ワークフロー

   バージョン 5.11 プラットフォームから移行する場合は、ワークフローランタイムディレクトリを制御する必要があります。 詳しくは、[ ワークフロー ](../../migration/using/specific-configurations-in-v5-11.md#workflows) の節を参照してください。

* トラッキング

   バージョン 5.11 プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 詳しくは、[ 追跡 ](../../migration/using/specific-configurations-in-v5-11.md#tracking) の節を参照してください。

* ホームページ

   v6.02 プラットフォームから移行する場合は、古いホームページを v6.02 から保持するための追加のパラメーターを定義できます。詳しくは、[ 使いやすさを参照してください。ホームページとナビゲーション ](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation) セクション。

* インタラクション

   **インタラクション** を使用する場合は、移行後に任意のパラメータを調整する必要があります。 詳しくは、[ インタラクション ](../../migration/using/general-configurations.md#interaction) の節を参照してください。
