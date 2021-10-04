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

この節では、v5.11 からの移行時に必要な追加設定について詳しく説明します。[ 一般設定 ](../../migration/using/general-configurations.md) の節で詳しく説明する設定もおこなう必要があります。

## web アプリケーション {#web-applications}

移行中、次の警告が自動的に表示されます。

```
The webApp ids have been modified during the migration process. Please make sure to check your scripts/css for broken compatibility (any client side JavaScript or css dealing directly with another element through its id is impacted). See file 'c:\svn\602\nl\build\ncs\var\upgrade/postupgrade/webAppsMigration_*************.txt' for details about the references that were automatically updated, if any.
```

Web アプリケーションの一部のコンポーネント（例えば、様々な数式フィールド）には、 @id属性が含まれています。 これらは Web アプリケーションの XML コードで使用され、同じ方法では生成されなくなりました。 これらはインターフェイスに表示されず、通常は使用しないでください。 ただし、場合によっては、@id属性を使用して、Web アプリケーションのレンダリングをパーソナライズすることができます。例えば、スタイルシートや JavaScript コードを使用する場合などです。

移行中は、警告で指定したログファイルのパスを **確認する必要があります。**

* **ファイルが空ではない**:移行前に記録された不整合や、まだ存在する問題に関する警告が含まれます。これは、存在しない ID を参照する Web アプリケーションの JavaScript コードです。 各エラーを確認し、修正する必要があります。
* **ファイルが空です**。これは、Adobe Campaignが問題を検出していないことを意味します。

ファイルが空かどうかに関係なく、これらの ID が他の場所での設定に使用されていないことを確認する必要があります（その場合は設定を適応させます）。

## ワークフロー {#workflows}

Adobe Campaignのインストールディレクトリの名前が変更されたので、移行後、一部のワークフローが機能しない場合があります。 ワークフローがそのアクティビティの 1 つで nl5 ディレクトリを参照する場合、エラーが発生します。 この参照を **build** に置き換えます。 SQL クエリを実行して、これらのワークフローを識別できます（PostgreSQL の例）。

```
SELECT   iWorkflowId, sInternalName, sLabel 
FROM XtkWorkflow 
WHERE mData LIKE '%nl5%';
```

## 使いやすさ {#user-friendliness}

Adobe Campaign v5.11 のホームページは使用できなくなりました。

お勧めしませんが、Adobe Campaign v5.11 からの特定のインターフェイスを維持したい場合は、特定のソリューションがあります。詳細については、お問い合わせください。

## MySQL {#mysql}

>[!IMPORTANT]
>
>MySQL は、バージョン 6.02 または 5.11 からこのエンジンを使用して移行する際に、メインデータベースエンジンとして v7 でのみサポートされます。

MySQL は、デフォルトではタイムゾーンを管理しません。 タイムゾーン管理を有効にするには、次のコマンドを実行します。

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root mysql
```

>[!NOTE]
>
>詳しくは、[https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html) を参照してください。

データベース構造に変更が加えられた場合、例えば設定（特定のインデックスの作成、SQL ビューの作成など）、移行時にいくつかの注意事項を講じる必要があります。 実際、移行手順との非互換性から、特定の変更が生成される場合があります。 例えば、**Timestamp** フィールドを含む SQL ビューを作成する場合、**usetimestamptz** オプションとの互換性はありません。 そのため、次の推奨事項に従うことをお勧めします。

1. 移行を開始する前に、データベースをバックアップします。
1. SQL の変更を削除します。
1. [Adobe Campaign 7 への移行の前提条件 ](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) の節で説明されている手順に従って、ポストアップグレードを実行します。
   >[!NOTE]
   >
   >[Adobe Campaign 7 への移行の前提条件 ](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) の節に示す移行手順に従う必要があります。
1. SQL の変更を再統合します。

この例では、**NmcTrackingLogMessages** ビューが作成され、**tslog** という名前の **Timestamp** フィールドが含まれています。 この場合、移行手順は失敗し、次のエラーメッセージが表示されます。

```
2011-10-04 11:57:51.804Z B67B28C0 1 info log Updating table 'NmcTrackingLogMessages'
2011-10-04 11:57:51.804Z B67B28C0 1 error log PostgreSQL error: ERROR: cannot alter type of a column used by a view or rule\nDETAIL: rule _RETURN on view nmctrackinglogmessagesview depends on column "tslog"\n (iRc=-2006)
2011-10-04 11:57:51.804Z B67B28C0 1 error log SQL order 'ALTER TABLE NmcTrackingLogMessages ALTER COLUMN tsLog TYPE TIMESTAMPTZ' was not executed. (iRc=-2006)
```

ポストアップグレードが確実に機能するようにするには、移行前にビューを削除し、移行後に TIMESTAMP WITH TIMEZONE モードに適応させながら再作成する必要があります。

## トラッキング {#tracking}

トラッキングの数式が変更されました。 移行時に、古い式 (v5) が新しい式 (v7) に置き換えられます。 Adobe Campaign v5 でパーソナライズされた数式を使用する場合、この設定は、Adobe Campaign v7 （**NmsTracking_ClickFormula** および **NmsTracking_OpenFormula** オプション）で適応する必要があります。

Web トラッキング管理も変更されました。 v7 への移行が完了したら、デプロイウィザードを起動して Web トラッキングの設定を完了する必要があります。

![](assets/migration_web_tracking.png)

次の 3 つのモードを選択できます。

* **セッション Web トラッキング**:リードスペー **** ジがインストールされていない場合は、このオプションがデフォルトで選択されます。このオプションは、パフォーマンスの面で最も理想的で、トラッキングログのサイズを制限できます。
* **永続的な Web トラッキング**
* **匿名 Web トラッキング**:リードスペー **** ジがインストールされている場合は、このオプションがデフォルトで選択されます。リソースを最も消費するオプションです。 上記のように、 **sSourceId** 列は（追跡テーブルと **CrmIncomingLead** テーブルで）インデックスを作成する必要があります。

>[!NOTE]
>
>これらの 3 つのモードの詳細は、[ この節 ](../../configuration/using/about-web-tracking.md) を参照してください。

## Adobe Campaign v7 ツリー構造 {#campaign-vseven-tree-structure}

移行中、ツリー構造は v7 標準に基づいて自動的に再編成されます。 新しいフォルダーが追加され、古いフォルダーが削除され、その内容が「移動する」フォルダーに配置されます。 移行後に、このフォルダー内の項目をすべて確認する必要があります。また、コンサルタントは、この項目を保持するか、削除するかを決定する必要があります。 保管するアイテムは、適切な場所に移動する必要があります。

ナビゲーションツリーの自動移行を無効にするオプションが追加されました。 この操作は手動で行われます。 古いフォルダーは削除されず、新しいフォルダーは追加されません。 このオプションは、標準の v5 ナビゲーションツリーに対して、多くの変更が加えられた場合にのみ使用してください。 移行前に、**[!UICONTROL 管理/オプション]** ノードで、コンソールにオプションを追加します。

* 内部名：NlMigration_KeepFolderStructure
* データタイプ：整数
* 値（テキスト）:1

このオプションを使用する場合、移行後に古いフォルダーを削除し、新しいフォルダーを追加して、必要なチェックをすべて実行する必要があります。

**新しいフォルダーの一覧**:

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
| nmsMRM | MRM | MRM がインストールされる |
| nmsOperations | キャンペーン | Campaign のインストール |

**古いフォルダーの一覧**:

移行後に削除される古いフォルダーは次のとおりです。

>[!NOTE]
>
>古いフォルダーの内容全体をチェックする必要があり、項目ごとに、コンサルタントがその内容を保持するか削除するかを決定します。 保管するアイテムは、適切な場所に移動する必要があります。

| 内部名 | ラベル | 条件 |
|---|---|---|
| nmsAdministration | 管理 | - |
| nmsDeliveryMgt | キャンペーンの実行 | - |
| ncmContent | コンテンツ管理 | Content Manager がインストールされている |
| ncmForm | 入力フォーム | Content Manager がインストールされている |
| ncmImage | 画像 | Content Manager がインストールされている |
| ncmJavascript | JavaScript コード | Content Manager がインストールされている |
| ncmJst | JavaScript テンプレート | Content Manager がインストールされている |
| ncmParameters | 設定 | Content Manager がインストールされている |
| ncmSrcSchema | データスキーマ | Content Manager がインストールされている |
| ncmStylesheet | XSL スタイルファイル | Content Manager がインストールされている |
| nmsAdminPlan | 管理 | Campaign のインストール |
| nmsResourcePlan | リソース | Campaign のインストール |
| nmsResourcesModels | テンプレート | Campaign のインストール |
| nmsRootPlan | キャンペーン管理 | Campaign のインストール |
| nmsOperator | マーケティングオペレーター | MRM がインストールされる |
