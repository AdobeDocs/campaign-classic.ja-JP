---
product: campaign
title: 設定の適応
description: Campaign v7 への移行の前後に設定を適応させる方法を説明します。
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: ad71dead-c0ca-42d5-baa8-0f340979231a
source-git-commit: 327f220d6700242308ef3738a38cc95b970e3f46
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 5%

---

# 設定の適応{#configuring-your-platform}

![](../../assets/v7-only.svg)

Adobe Campaign v7 の大きな変更の一部には、特定の設定が必要です。 これらの設定は、移行の前または後に必要になる場合があります。

Campaign v5 または v6 からの移行時にAdobe Campaign v7 で実行する詳細な設定は、 [このページ](general-configurations.md).


移行中に、 **NmsRecipient** スキーマ定義からテーブルが再構築されます。 このテーブルの SQL 構造に対してAdobe Campaign以外で行われた変更は失われます。

チェックする要素の例：

* 列（またはインデックス）を **NmsRecipient** テーブルが作成されましたが、スキーマで詳細を指定していない場合、これは保存されません。
* この **テーブル領域** 属性は、デフォルトで、その値を取り戻します。つまり、デプロイウィザードで定義された値です。
* 参照ビューを **NmsRecipient** テーブルの上にマウスポインターを置いて、移行する前に削除する必要があります。


## 移行前 {#before-the-migration}

Adobe Campaign v7 に移行する際に、次の要素を設定する必要があります。 これらの要素は、 **postupgrade**.

* タイムゾーン

   v5.11 プラットフォームからの移行中に、ポストアップグレード中に使用するタイムゾーンを指定する必要があります。

   「マルチタイムゾーン」モードを使用する場合は、 [この節](../../migration/using/general-configurations.md#time-zones).

   oracleをデータベースとして使用する場合は、アプリケーションサーバーとOracleサーバーの間で、データベースタイムゾーンファイルが正しく同期されていることを確認します。 [詳細情報](../../migration/using/general-configurations.md#oracle)

* セキュリティゾーン

   セキュリティ上の理由により、Adobe Campaignプラットフォームは、デフォルトではアクセスできなくなりました。セキュリティゾーンを設定する必要があります。この場合、移行前にユーザー IP アドレスを収集する必要があります。 [詳細情報](../../migration/using/general-configurations.md#security)

* 構文

   一部の JavaScript コードは、新しいインタープリターを使用するため、v7 バージョンでは受け入れられなくなる場合があります。 [詳細情報](../../migration/using/general-configurations.md#javascript)。

   同様に、SQLData ベースの構文を置き換える新しい構文がAdobe Campaign v7 で導入されました。 コード要素をこの構文で使用する場合は、適応させる必要があります。 [詳細情報](../../migration/using/general-configurations.md#sqldata)

* パスワード

   次の項目を設定する必要があります。 **管理者** および **内部** パスワード。 [詳細情報](../../migration/using/before-starting-migration.md#user-passwords)

* ツリー構造

   v5.11 プラットフォームから移行する場合は、Adobe Campaign v6 の規則に従ってツリー構造フォルダーを再編成する必要があります。 [詳細情報](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11)。

* インタラクション

   Campaign v6.02 から移行し、  **インタラクション** モジュールの場合、v7 に存在しなくなった 6.02 スキーマ参照をすべて削除する必要があります。 [詳細情報](../../migration/using/general-configurations.md#interaction)

## 移行後 {#after-the-migration}

実行後 **postupgrade**、次の要素を確認して設定します。

* ミラーページ

   ミラーページのパーソナライゼーションブロックが v6.x で変更されました。この新しいバージョンでは、これらのページにアクセスする際のセキュリティが向上します。

   メッセージで v5 パーソナライゼーションブロックを使用している場合、ミラーページの表示に失敗します。 Adobeでは、メッセージにミラーページを挿入する際に新しいパーソナライゼーションブロックを使用することを強くお勧めします。

   ただし、一時的な回避策として（また、ミラーページがまだ有効な状態のまま）、古いパーソナライゼーションブロックに戻すと、オプションを変更してこの問題を回避できます **[!UICONTROL XtkAcceptOldPasswords]** を設定し、 **[!UICONTROL 1]**. この変更は、新しい v6.x パーソナライゼーションブロックの使用には影響しません。

* 構文

   構文に関するエラーが発生した場合は、アップグレード後に、 **allowSQLInjection** オプション **serverConf.xml** ファイルを書き換える時間を提供します。 コードを変更したら、必ずセキュリティを再アクティブ化してください。 [詳細情報](../../migration/using/general-configurations.md#sqldata)

* 競合

   移行はポストアップグレードを通じて実行され、レポート、フォーム、Web アプリケーションに競合が表示される場合があります。 これらの競合は、コンソールから解決できます。 [詳細情報](../../migration/using/general-configurations.md#conflicts)

* Tomcat

   インストールフォルダーをカスタマイズした場合は、移行後に正しく更新されていることを確認してください。 [詳細情報](../../migration/using/general-configurations.md#tomcat)

* レポート

   すべての標準レポートで、現在 v6.x レンダリングエンジンが使用されています。 レポートに JavaScript コードを追加していた場合は、一部の要素が影響を受ける可能性があります。 [詳細情報](../../migration/using/general-configurations.md#reports)

* Web アプリケーション

   アップグレード後に、識別された Web アプリケーションへの接続で問題が発生した場合は、 **allowUserPassword** および **sessionTokenOnly** オプション **serverConf.xml** ファイル。 セキュリティ上の問題を回避するには、問題が解決した後に、次の 2 つのオプションを再度アクティブ化する必要があります。 [詳細情報](../../migration/using/general-configurations.md#identified-web-applications)

   Web アプリケーションのタイプと設定に応じて、追加の操作を実行して、Web アプリケーションが正しく機能するようにする必要があります。 [詳細情報](../../migration/using/general-configurations.md#web-applications)

   v5.11 プラットフォームから移行する場合は、追加の設定を実行する必要があります。 [詳細情報](../../migration/using/general-configurations.md#specific-configurations-in-v5-11.md)

* セキュリティゾーン

   サーバーを起動する前に、セキュリティゾーンを設定する必要があります。 [詳細情報](../../installation/using/security-zones.md) および [こちらを参照](../../migration/using/general-configurations.md#security)

* ワークフロー

   v5.11 プラットフォームから移行する場合は、 workflows フォルダーを確認する必要があります。 [詳細情報](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11)

* トラッキング

   v5.11 プラットフォームから移行する場合は、トラッキングモードを設定する必要があります。 [詳細情報](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11)

* インタラクション

   次を使用する場合、 **インタラクション**&#x200B;を使用する場合、移行後にパラメーターを調整する必要があります。 [詳細情報](../../migration/using/general-configurations.md#interaction)

* ダッシュボード

   クライアントエラーが表示された場合は、新しいAdobe Campaign v7 コードでダッシュボードを更新するか、次のファイルを v6.02 インスタンスから v7 インスタンスに手動でコピーする必要があります。

   ```
   v6.02 files and spaces:
   /usr/local/neolane/nl6/datakit/xtk/eng/css/dropDownMenu.css
   /usr/local/neolane/nl6/datakit/xtk/eng/js/client/dropDownMenu.js
   v6.1 files and spaces:
   /usr/local/neolane/nl6/deprecated/xtk/css/dropDownMenu.css
   /usr/local/neolane/nl6/deprecated/xtk/js/client/dropDownMenu.js  
   ```


## v5.11 から v7 までの特定の設定{#specific-configurations-in-v5-11}

![](../../assets/v7-only.svg)

この節では、v5.11 からの移行時に必要となる追加の設定について詳しく説明します。また、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

### web アプリケーション {#web-applications-v5}

移行中は、次の警告が自動的に表示されます。

```
The webApp ids have been modified during the migration process. Please make sure to check your scripts/css for broken compatibility (any client side JavaScript or css dealing directly with another element through its id is impacted). See file 'c:\svn\602\nl\build\ncs\var\upgrade/postupgrade/webAppsMigration_*************.txt' for details about the references that were automatically updated, if any.
```

Web アプリケーションの一部のコンポーネント（例えば、様々な数式フィールド）には、 @id属性が含まれています。 これらは Web アプリケーションの XML コードで使用され、同じ方法で生成されなくなりました。 これらはインターフェイスには表示されず、通常は使用しないでください。 ただし、場合によっては、 @id属性を使用して、Web アプリケーションのレンダリングをパーソナライズすることができます。例えば、スタイルシートを介したり、JavaScript コードを使用したりします。

移行中に、 **必須** 警告で指定したログファイルのパスを確認します。

* **ファイルが空ではありません**:移行前に記録された不整合と、まだ存在する問題を懸念する警告が含まれます。 これは、存在しない ID を参照する Web アプリケーションの JavaScript コードです。 それぞれのエラーを確認し、修正する必要があります。
* **ファイルが空です**:これは、Adobe Campaignが問題を検出していないことを意味します。

ファイルが空かどうかに関わらず、これらの ID が他の場所での設定に使用されていないことを確認する必要があります（その場合は設定を適応させます）。

### ワークフロー {#workflows}

Adobe Campaignインストールディレクトリの名前が変更されたので、移行後に一部のワークフローが機能しない場合があります。 ワークフローがそのアクティビティの 1 つで nl5 ディレクトリを参照している場合、エラーが発生します。 この参照を次で置き換えます。 **ビルド**. SQL クエリを実行して、これらのワークフローを識別できます（PostgreSQL の例）。

```
SELECT   iWorkflowId, sInternalName, sLabel 
FROM XtkWorkflow 
WHERE mData LIKE '%nl5%';
```

### MySQL {#mysql}

>[!CAUTION]
>
>MySQL は、このエンジンを使用してバージョン 6.02 または 5.11 から移行する際に、v7 でメインデータベースエンジンとしてのみサポートされます。

MySQL は、デフォルトではタイムゾーンを管理しません。 タイムゾーン管理を有効にするには、次のコマンドを実行します。

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root mysql
```

>[!NOTE]
>
>詳しくは、 [https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html) ページ。

データベース構造に変更が加えられた場合（例えば、特定のインデックスの作成、SQL ビューの作成など）、移行時に注意が必要です。 実際、移行手順との非互換性から、特定の変更が生成される場合があります。 例えば、次を含む SQL ビューを作成します。 **タイムスタンプ** フィールドは **usetimestamptz** オプション。 したがって、次の推奨事項に従うことをお勧めします。

1. 移行を開始する前に、データベースをバックアップします。
1. SQL の変更を削除します。
1. アップグレード後の実行
   >[!NOTE]
   >
   >次に示す移行手順に従う必要があります。 [この節](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md).
1. SQL の変更を再統合します。

この例では、 **NmcTrackingLogMessages** ビューが作成され、これには次のアイテムが含まれています： **タイムスタンプ** フィールド名 **tslog**. この場合、移行手順は失敗し、次のエラーメッセージが表示されます。

```
2011-10-04 11:57:51.804Z B67B28C0 1 info log Updating table 'NmcTrackingLogMessages'
2011-10-04 11:57:51.804Z B67B28C0 1 error log PostgreSQL error: ERROR: cannot alter type of a column used by a view or rule\nDETAIL: rule _RETURN on view nmctrackinglogmessagesview depends on column "tslog"\n (iRc=-2006)
2011-10-04 11:57:51.804Z B67B28C0 1 error log SQL order 'ALTER TABLE NmcTrackingLogMessages ALTER COLUMN tsLog TYPE TIMESTAMPTZ' was not executed. (iRc=-2006)
```

アップグレード後の動作を確実におこなうには、移行前にビューを削除し、移行後に再作成し、TIMESTAMP WITH TIMEZONE モードに適応させる必要があります。

### トラッキング {#tracking}

トラッキング式が変更されました。 移行時に、古い式 (v5) が新しい式 (v7) に置き換えられます。 Adobe Campaign v5 でパーソナライズされた数式を使用する場合、この設定はAdobe Campaign v7 (**NmsTracking_ClickFormula** および **NmsTracking_OpenFormula** オプション )。

Web トラッキング管理も変更されました。 v7 への移行が完了したら、デプロイウィザードを起動して、Web トラッキングの設定を完了する必要があります。

![](assets/migration_web_tracking.png)

次の 3 つのモードを選択できます。

* **セッション Web トラッキング**:この **[!UICONTROL リード]** パッケージがインストールされていません。このオプションはデフォルトで選択されています。 このオプションは、パフォーマンスの点で最も理想的で、トラッキングログのサイズを制限できます。
* **永続的な Web トラッキング**
* **匿名 Web トラッキング**:この **[!UICONTROL リード]** パッケージがインストールされている場合、このオプションはデフォルトで選択されています。 リソースを最も消費するオプションです。 上記のように、 **sSourceId** 列のインデックスを作成する必要があります ( トラッキングテーブル内で **CrmIncomingLead** 表 )。

>[!NOTE]
>
>これらの 3 つのモードについて詳しくは、 [この節](../../configuration/using/about-web-tracking.md).

### Adobe Campaign v7 ツリー構造 {#campaign-vseven-tree-structure}

移行中、ツリー構造は v7 標準に基づいて自動的に再編成されます。 新しいフォルダが追加され、古いフォルダが削除され、その内容が「移動する」フォルダに配置されます。 移行後に、このフォルダー内の項目をすべてチェックする必要があります。また、コンサルタントは、このフォルダーを保持するか、各項目を削除するかを決定する必要があります。 保持する項目は、適切な場所に移動する必要があります。

ナビゲーションツリーの自動移行を無効にするオプションが追加されました。 この操作は手動で行われました。 古いフォルダーは削除されず、新しいフォルダーは追加されません。 このオプションは、標準の v5 ナビゲーションツリーで、多くの変更がおこなわれている場合にのみ使用してください。 移行前に、コンソールにオプションを追加します。 **[!UICONTROL 管理/オプション]** ノード：

* 内部名：NlMigration_KeepFolderStructure
* データタイプ：整数
* 値（テキスト） :1

このオプションを使用する場合、移行後に古いフォルダーを削除し、新しいフォルダーを追加して、必要なチェックをすべて実行する必要があります。

**新しいフォルダーのリスト**:

移行後に、次のフォルダーを追加する必要があります。

| 内部名 | ラベル | 条件 |
|---|---|---|
| nmsAutoObjects | 自動作成されたオブジェクト | - |
| nmsCampaignAdmin | キャンペーン管理 | - |
| nmsCampaignMgt | キャンペーン管理 | - |
| nmsCampaignRes | キャンペーン管理 | - |
| nmsModels | テンプレート | - |
| nmsOnlineRes | オンライン | - |
| nmsProduction | Production（本番） | - |
| nmsProfilProcess | プロセス | - |
| xtkDashboard | ダッシュボード | - |
| xtkPlatformAdmin | プラットフォーム | - |
| nmsLocalOrgUnit | 組織単位 | - |
| nmsMRM | MRM | MRM がインストールされました |
| nmsOperations | キャンペーン | インストール済みキャンペーン |

**古いフォルダーのリスト**:

移行後に削除される古いフォルダーは次のとおりです。

>[!NOTE]
>
>古いフォルダーの内容全体をチェックする必要があり、項目ごとに、コンサルタントがそのフォルダーを保持するか削除するかを決定します。 保持する項目は、適切な場所に移動する必要があります。

| 内部名 | ラベル | 条件 |
|---|---|---|
| nmsAdministration | 管理 | - |
| nmsDeliveryMgt | キャンペーンの実行 | - |
| ncmContent | コンテンツ管理 | Content Manager がインストールされました |
| ncmForm | 入力フォーム | Content Manager がインストールされました |
| ncmImage | 画像 | Content Manager がインストールされました |
| ncmJavascript | JavaScript コード | Content Manager がインストールされました |
| ncmJst | JavaScript テンプレート | Content Manager がインストールされました |
| ncmParameters | 設定 | Content Manager がインストールされました |
| ncmSrcSchema | データスキーマ | Content Manager がインストールされました |
| ncmStylesheet | XSL スタイルファイル | Content Manager がインストールされました |
| nmsAdminPlan | 管理 | インストール済みキャンペーン |
| nmsResourcePlan | リソース | インストール済みキャンペーン |
| nmsResourcesModels | テンプレート | インストール済みキャンペーン |
| nmsRootPlan | キャンペーン管理 | インストール済みキャンペーン |
| nmsOperator | マーケティングオペレーター | MRM がインストールされました |


## v6.02 から v7 に固有の設定{#specific-configurations-in-v6-02}

![](../../assets/v7-only.svg)

次の節では、v6.02 からの移行時に必要となる追加の設定について詳しく説明します。詳しくは、 [このページ](../../migration/using/general-configurations.md).

### web アプリケーション {#web-applications-v6}

v6.02 から移行する場合、概要タイプの Web アプリケーションに関するエラーログが表示されることがあります。 エラーメッセージの例：

```
[PU-0006] Entity of type : 'xtk:entityBackupNew' and Id 'nms:webApp|taskOverview', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'xtk:formDictionary' and Id 'nms:webApp|lastTasks', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'nms:webApp' and Id 'taskOverview', expression '[SQLDATA[' was found : '...@owner-id] IN ([SQLDATA[select iGroupid...'. (iRc=-1)
```

これらの Web アプリケーションは SQLData を使用しており、セキュリティが高まるので v7 との互換性がありません。 これらのエラーは、移行エラーにつながります。

これらの Web アプリケーションを使用しなかった場合は、次のクリーンアップスクリプトを実行し、ポストアップグレードを再実行します。

```
Nlserver javascript -instance:[instance_name] -file [installation_path]/datakit/xtk/fra/js/removeOldWebApp.js
```

これらの Web アプリケーションを変更済みで、v7 で引き続き使用する場合は、 **allowSQLInjection** 」オプションを使用し、アップグレード後に再起動します。 詳しくは、 [SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

### Message Center {#message-center}

Message Center コントロールインスタンスの移行後は、トランザクションメッセージテンプレートを再公開して、機能させる必要があります。

v7 では、実行インスタンス上のトランザクションメッセージテンプレートの名前が変更されました。 現在は、作成元のコントロールインスタンスに対応するオペレーター名のプレフィックスが付いています。例： **control1_template1_rt** ( **control1** は演算子の名前です )。 大量のテンプレートがある場合は、コントロールインスタンス上の古いテンプレートを削除することをお勧めします。