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

Adobe Campaign v7 の大きな変更の一部では、有効な操作を確実におこなうために、設定が必要です。 これらのパラメーターは、移行の前または後に必要になる場合があります。 この節では、変更とその設定モードについて説明します。

移行中に、 **NmsRecipient** スキーマ定義からテーブルが再構築されます。 このテーブルの SQL 構造に対してAdobe Campaign以外で行われた変更は失われます。

チェックする要素の例：

* 列（またはインデックス）を **NmsRecipient** テーブルが作成されましたが、スキーマで詳細を指定していない場合、これは保存されません。
* この **テーブル領域** 属性は、デフォルトで、その値を取り戻します。つまり、デプロイウィザードで定義された値です。
* NmsRecipient テーブルに参照ビューを追加した場合は、移行前に削除する必要があります。

この警告は、Oracleユーザーにも影響します。( **usetimestamptz:1** オプション ( [タイムゾーン](../../migration/using/general-configurations.md#time-zones))、少なくとも 1 つの **日付+時刻** フィールドが再構築されます。

## 移行前 {#before-the-migration}

Adobe Campaign v7 に移行する際に、次の要素を設定する必要があります。 これらの要素は、 **postupgrade**.

* タイムゾーン

   v5.11 プラットフォームからの移行中に、ポストアップグレード中に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) 」セクションに入力します。

   oracleをデータベースとして使用する場合は、アプリケーションサーバーとOracleサーバーの間で、データベースタイムゾーンファイルが正しく同期されていることを確認します。 詳しくは、 [Oracle](../../migration/using/general-configurations.md#oracle) 」セクションに入力します。

* セキュリティゾーン

   セキュリティ上の理由により、Adobe Campaignプラットフォームは、デフォルトではアクセスできなくなりました。セキュリティゾーンを設定する必要があります。この場合、移行前にユーザー IP アドレスを収集する必要があります。

   詳しくは、 [セキュリティ](../../migration/using/general-configurations.md#security) 」セクションに入力します。

* 構文

   JavaScript の特定の構文は、バージョン 5.11 および 6.02 で受け入れられ、新しいインタープリターの使用により v7 バージョンでは受け入れられなくなる場合があります。 詳しくは、 [JavaScript](../../migration/using/general-configurations.md#javascript) 」セクションに入力します。

   同様に、SQLData ベースの構文を置き換える新しい構文がAdobe Campaign v7 で導入されました。 コード要素をこの構文で使用する場合は、適応させる必要があります。 詳しくは、 [SQLData](../../migration/using/general-configurations.md#sqldata) 」セクションに入力します。

* パスワード

   次の項目を設定する必要があります。 **管理者** および **内部** パスワード。 詳しくは、 [ユーザーパスワード](../../migration/using/before-starting-migration.md#user-passwords) 」セクションに入力します。

* ツリー構造

   v5.11 プラットフォームから移行する場合は、Adobe Campaign v6 の規則に従ってツリー構造フォルダーを再編成する必要があります。 詳しくは、 [Adobe Campaign v7 ツリー構造](../../migration/using/specific-configurations-in-v5-11.md#campaign-vseven-tree-structure) 」セクションに入力します。

* インタラクション

   次を使用する場合、 **インタラクション**&#x200B;の場合は、v7 に存在しない 6.02 スキーマ参照をすべて削除する必要があります。 詳しくは、 [インタラクション](../../migration/using/general-configurations.md#interaction) 」セクションに入力します。

## 移行後 {#after-the-migration}

実行後 **postupgrade**&#x200B;の場合、次の要素を考慮に入れ、対応する設定を実行する必要があります。

* ミラーページ

   ミラーページのパーソナライゼーションブロックが v6.x で変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージで v5 パーソナライゼーションブロックを使用している場合、ミラーページの表示に失敗します。 Adobeでは、メッセージにミラーページを挿入する際に新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的なソリューション（およびミラーページがまだ有効な状態である場合）として、古いパーソナライゼーションブロックに戻すと、オプションを変更してこの問題を回避できます **[!UICONTROL XtkAcceptOldPasswords]** を設定し、 **[!UICONTROL 1]**. この変更は、新しい v6.x パーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関するエラーが発生した場合は、アップグレード後に、 **allowSQLInjection** オプション **serverConf.xml** ファイルを書き換える時間を提供します。 コードを変更したら、必ずセキュリティを再アクティブ化してください。 詳しくは、 [SQLData](../../migration/using/general-configurations.md#sqldata) 」セクションに入力します。

* 競合

   移行はポストアップグレードを通じて実行され、レポート、フォーム、Web アプリケーションに競合が表示される場合があります。 これらの競合は、コンソールから解決できます。

   詳しくは、 [競合](../../migration/using/general-configurations.md#conflicts) 」セクションに入力します。

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 詳しくは、 [Tomcat](../../migration/using/general-configurations.md#tomcat) 」セクションに入力します。

* レポート

   すべての標準レポートで、現在 v6.x レンダリングエンジンが使用されています。 レポートに JavaScript コードを追加していた場合は、一部の要素が変更される場合があります。

   詳しくは、 [レポート](../../migration/using/general-configurations.md#reports) 」セクションに入力します。

* Web アプリケーション

   アップグレード後に、識別された Web アプリケーションへの接続で問題が発生した場合は、 **allowUserPassword** および **sessionTokenOnly** オプション **serverConf.xml** ファイル。 この 2 つのオプションは、必ず無効にしてください。 詳しくは、 [特定された Web アプリケーション](../../migration/using/general-configurations.md#identified-web-applications) 」セクションに入力します。

   Web アプリケーションのタイプと設定に応じて、追加の操作を実行して、Web アプリケーションが正しく機能するようにする必要があります。

   詳しくは、 [Web アプリケーション](../../migration/using/general-configurations.md#web-applications) 」セクションに入力します。

   v5.11 プラットフォームから移行する場合は、次の追加設定を実行する必要があります。詳しくは、 [Web アプリケーション](../../migration/using/specific-configurations-in-v5-11.md#web-applications) 」セクションに入力します。

* セキュリティゾーン.

   サーバーを起動する前に、セキュリティゾーンを設定する必要があります。 詳しくは、 [この節](../../installation/using/security-zones.md) そして [セキュリティ](../../migration/using/general-configurations.md#security) 」セクションに入力します。

* スキーマ

   Red Hat では、特定のスキーマを編集する際にエラーが発生する場合があります。 詳しくは、 [Red-Hat](../../migration/using/general-configurations.md#red-hat) 」セクションに入力します。

* ワークフロー

   v5.11 プラットフォームから移行する場合は、ワークフローランタイムディレクトリを制御する必要があります。 詳しくは、 [ワークフロー](../../migration/using/specific-configurations-in-v5-11.md#workflows) 」セクションに入力します。

* トラッキング

   v5.11 プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 詳しくは、 [トラッキング](../../migration/using/specific-configurations-in-v5-11.md#tracking) 」セクションに入力します。

* ホームページ

   v6.02 プラットフォームから移行する場合、v6.02 から古いホームページを維持するための追加のパラメーターを定義できます。詳しくは、 [使いやすさ：ホームページとナビゲーション](../../migration/using/specific-configurations-in-v6-02.md#user-friendliness--home-page-and-navigation) 」セクションに入力します。

* インタラクション

   次を使用する場合、 **インタラクション**&#x200B;を使用する場合、移行後にパラメーターを調整する必要があります。 詳しくは、 [インタラクション](../../migration/using/general-configurations.md#interaction) 」セクションに入力します。
