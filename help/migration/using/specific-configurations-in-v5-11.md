---
product: campaign
title: v5.11 特有の設定
description: v5.11 特有の設定
audience: migration
content-type: reference
topic-tags: configuration
exl-id: 978e1249-f79b-4f5f-9a94-3bb2510785de
source-git-commit: e719c8c94f1c08c6601b3386ccd99d250c9e606b
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 5%

---

# v5.11 特有の設定{#specific-configurations-in-v5-11}

![](../../assets/v7-only.svg)

この節では、v5.11 からの移行時に必要となる追加の設定について詳しく説明します。また、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

## web アプリケーション {#web-applications}

移行中は、次の警告が自動的に表示されます。

```
The webApp ids have been modified during the migration process. Please make sure to check your scripts/css for broken compatibility (any client side JavaScript or css dealing directly with another element through its id is impacted). See file 'c:\svn\602\nl\build\ncs\var\upgrade/postupgrade/webAppsMigration_*************.txt' for details about the references that were automatically updated, if any.
```

Web アプリケーションの一部のコンポーネント（例えば、様々な数式フィールド）には、 @id属性が含まれています。 これらは Web アプリケーションの XML コードで使用され、同じ方法で生成されなくなりました。 これらはインターフェイスには表示されず、通常は使用しないでください。 ただし、場合によっては、 @id属性を使用して、Web アプリケーションのレンダリングをパーソナライズすることができます。例えば、スタイルシートを介したり、JavaScript コードを使用したりします。

移行中に、 **必須** 警告で指定したログファイルのパスを確認します。

* **ファイルが空ではありません**:移行前に記録された不整合と、まだ存在する問題を懸念する警告が含まれます。 これは、存在しない ID を参照する Web アプリケーションの JavaScript コードです。 それぞれのエラーを確認し、修正する必要があります。
* **ファイルが空です**:これは、Adobe Campaignが問題を検出していないことを意味します。

ファイルが空かどうかに関わらず、これらの ID が他の場所での設定に使用されていないことを確認する必要があります（その場合は設定を適応させます）。

## ワークフロー {#workflows}

Adobe Campaignインストールディレクトリの名前が変更されたので、移行後に一部のワークフローが機能しない場合があります。 ワークフローがそのアクティビティの 1 つで nl5 ディレクトリを参照している場合、エラーが発生します。 この参照を次で置き換えます。 **ビルド**. SQL クエリを実行して、これらのワークフローを識別できます（PostgreSQL の例）。

```
SELECT   iWorkflowId, sInternalName, sLabel 
FROM XtkWorkflow 
WHERE mData LIKE '%nl5%';
```

## 使いやすさ {#user-friendliness}

Adobe Campaign v5.11 のホームページは使用できなくなりました。

非推奨ですが、Adobe Campaign v5.11 からの特定のインターフェイスを維持する場合は、特定のソリューションがあります。詳しくは、お問い合わせください。

## MySQL {#mysql}

>[!IMPORTANT]
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
1. アップグレード後に、  [Adobe Campaign 7 への移行の前提条件](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 」セクションに入力します。
   >[!NOTE]
   >
   >次に示す移行手順に必ず従ってください： [Adobe Campaign 7 への移行の前提条件](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 」セクションに入力します。
1. SQL の変更を再統合します。

この例では、 **NmcTrackingLogMessages** ビューが作成され、これには次のアイテムが含まれています： **タイムスタンプ** フィールド名 **tslog**. この場合、移行手順は失敗し、次のエラーメッセージが表示されます。

```
2011-10-04 11:57:51.804Z B67B28C0 1 info log Updating table 'NmcTrackingLogMessages'
2011-10-04 11:57:51.804Z B67B28C0 1 error log PostgreSQL error: ERROR: cannot alter type of a column used by a view or rule\nDETAIL: rule _RETURN on view nmctrackinglogmessagesview depends on column "tslog"\n (iRc=-2006)
2011-10-04 11:57:51.804Z B67B28C0 1 error log SQL order 'ALTER TABLE NmcTrackingLogMessages ALTER COLUMN tsLog TYPE TIMESTAMPTZ' was not executed. (iRc=-2006)
```

アップグレード後の動作を確実におこなうには、移行前にビューを削除し、移行後に再作成し、TIMESTAMP WITH TIMEZONE モードに適応させる必要があります。

## トラッキング {#tracking}

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

## Adobe Campaign v7 ツリー構造 {#campaign-vseven-tree-structure}

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
