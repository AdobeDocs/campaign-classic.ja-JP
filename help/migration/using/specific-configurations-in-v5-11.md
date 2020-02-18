---
title: v5.11での具体的な設定
seo-title: v5.11での具体的な設定
description: v5.11での具体的な設定
seo-description: null
page-status-flag: never-activated
uuid: d6920beb-a766-4aec-8a8e-d32e47b545a4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: configuration
discoiquuid: fc280640-528d-44de-87d8-52f443772abd
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9f7cf3d530f141a661df5fcc8cbcf0bb4c8d3e89

---


# v5.11での具体的な設定{#specific-configurations-in-v5-11}

この節では、v5.11からの移行時に必要な追加設定について説明します。また、「一般設定」セクションで詳しく説明されている設定も [行う必要があります](../../migration/using/general-configurations.md) 。

## Web アプリケーション {#web-applications}

移行中に、次の警告が自動的に表示されます。

```
The webApp ids have been modified during the migration process. Please make sure to check your scripts/css for broken compatibility (any client side javascript or css dealing directly with another element through its id is impacted). See file 'c:\svn\602\nl\build\ncs\var\upgrade/postupgrade/webAppsMigration_*************.txt' for details about the references that were automatically updated, if any.
```

様々な数式フィールドなど、Webアプリケーションの一部のコンポーネントには@id属性があります。 これらはWebアプリケーションのXMLコードで使用され、同じ方法で生成されることはなくなりました。 インターフェイスには表示されず、通常は使用しないでください。 ただし、@id属性を使用してWebアプリケーションのレンダリングをパーソナライズしたり、スタイルシートやJavaScriptコードを使用したりする場合もあります。

移行中に、警告 **で** 、次のログファイルのパスを確認する必要があります。

* **ファイルが空ではありません**:移行前に記録された不整合に関する警告と、現在も存在する警告が含まれます。 これは、存在しないIDを参照するWebアプリケーション内のJavaScriptコードにすることができます。 各エラーをチェックして修正する必要があります。
* **ファイルが空です**:つまり、Adobe Campaignで問題が検出されていません。

ファイルが空かどうかにかかわらず、これらのIDが他の場所での設定に使用されていないことを確認する必要があります（その場合は設定を適応させます）。

## ワークフロー {#workflows}

Adobe Campaignインストールディレクトリの名前が変更されているので、移行後に一部のワークフローが機能しない場合があります。 ワークフローがそのアクティビティの1つでnl5ディレクトリを参照する場合、エラーが発生します。 この参照を **buildに置き換えます**。 SQLクエリを実行して、次のワークフローを識別できます（PostgreSQLの例）。

```
SELECT   iWorkflowId, sInternalName, sLabel 
FROM XtkWorkflow 
WHERE mData LIKE '%nl5%';
```

## 使いやすさ {#user-friendliness}

Adobe Campaign v5.11のホームページは使用できなくなりました。

お勧めしませんが、Adobe Campaign v5.11から特定のインターフェイスを維持する場合は、特定の解決策があります。詳しくは、お問い合わせください。

## MySQL {#mysql}

>[!IMPORTANT]
>
>MySQLは、バージョン6.02または5.11からこのエンジンを使用して移行する場合に、メインデータベースエンジンとしてv7でのみサポートされます。

MySQLは、デフォルトでタイムゾーンを管理しません。 タイムゾーン管理を有効にするには、次のコマンドを実行します。

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root mysql
```

>[!NOTE]
>
>詳しくは、http://dev.mysql.com/doc/refman/5.5/en/time-zone-support.htmlページを参照して [ください](http://dev.mysql.com/doc/refman/5.5/en/time-zone-support.html) 。

データベース構造に変更が加えられた場合は、設定中（特定のインデックスの作成、SQLビューの作成など）、移行時に一定の注意を払う必要があります。 実際に、移行手順との互換性のない変更が生じる可能性があります。 例えば、 **Timestampフィールドを含むSQLビューを作成する場合** 、usetimestamptzオプションとは互換性が **ありません** 。 したがって、以下の推奨事項に従うことをお勧めします。

1. 移行を開始する前に、データベースをバックアップします。
1. SQLの変更を削除します。
1. 「Adobe Campaign 7への移行の前提条件」の手順に従っ [て、アップグレード後に実行します](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 。
   >[!NOTE]
   >
   >「Adobe Campaign 7への移行の前提条件」の節に示されている移 [行手順に従う必要があります](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 。
1. SQLの変更を再統合します。

この例では、 **NmcTrackingLogMessagesビューが作成され** 、「 **tslog** 」という名前の「 **Timestamp**」フィールドがあります。 この場合、移行手順は失敗し、次のエラーメッセージが表示されます。

```
2011-10-04 11:57:51.804Z B67B28C0 1 info log Updating table 'NmcTrackingLogMessages'
2011-10-04 11:57:51.804Z B67B28C0 1 error log PostgreSQL error: ERROR: cannot alter type of a column used by a view or rule\nDETAIL: rule _RETURN on view nmctrackinglogmessagesview depends on column "tslog"\n (iRc=-2006)
2011-10-04 11:57:51.804Z B67B28C0 1 error log SQL order 'ALTER TABLE NmcTrackingLogMessages ALTER COLUMN tsLog TYPE TIMESTAMPTZ' was not executed. (iRc=-2006)
```

アップグレード後の動作を確実にするには、移行前にビューを削除し、移行後にTIMESTAMP WITH TIMEZONEモードに適合させながら再作成する必要があります。

## トラッキング {#tracking}

トラッキング式が変更されました。 移行時に、古い数式(v5)が新しい数式(v7)に置き換えられます。 Adobe Campaign v5でパーソナライズされた数式を使用する場合、この設定をAdobe Campaign v7(**NmsTracking_ClickFormula** および **NmsTracking_OpenFormula** options)で適合させる必要があります。

Webトラッキング管理も変更されました。 v7への移行が完了したら、デプロイメントウィザードを起動してWeb追跡の設定を完了する必要があります。

![](assets/migration_web_tracking.png)

次の3つのモードを使用できます。

* **セッションWeb追跡**:パッケージがイ **[!UICONTROL Leads]** ンストールされていない場合、このオプションはデフォルトで選択されています。 このオプションは、パフォーマンスの点で最も理想的なオプションで、トラッキングログのサイズを制限できます。
* **恒久的なウェブトラッキング**
* **匿名Web追跡**:パッケージがイ **[!UICONTROL Leads]** ンストールされている場合、このオプションはデフォルトで選択されています。 これは、最もリソースを消費するオプションです。 上記のように、 **sSourceId列のインデックスは** (追跡テーブルとCrmIncomingLeadテーブル内で **** )作成する必要があります。

>[!NOTE]
>
>For more information on these three modes, refer to [this section](../../configuration/using/about-web-tracking.md).

## Adobe Campaign v7のツリー構造 {#campaign-vseven-tree-structure}

移行中、ツリー構造はv7標準に基づいて自動的に再構成されます。 新しいフォルダが追加され、古いフォルダが削除され、その内容が[移動先]フォルダに配置されます。 移行後にこのフォルダ内のすべての項目を確認する必要があり、コンサルタントはこの項目を保持するか、各項目を削除するかを決定する必要があります。 保管する物は正しい場所に移す必要がある。

ナビゲーションツリーの自動移行を無効にするオプションが追加されました。 この操作は現在手動です。 古いフォルダは削除されず、新しいフォルダは追加されません。 このオプションは、標準搭載のv5ナビゲーションツリーが多くの変更を加えた場合にのみ使用します。 移行前に、次のノードでコンソールにオプションを追加し **[!UICONTROL Administration > Options]** ます。

* 内部名：NlMigration_KeepFolderStructure
* データタイプ：整数
* 値（テキスト）:1

このオプションを使用する場合、移行後に古いフォルダを削除する必要があります。新しいフォルダを追加し、必要なチェックをすべて実行します。

**新しいフォルダのリスト**:

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
| nmsMRM | MRM | MRMがインストールされました |
| nmsOperations | キャンペーン | キャンペーンのインストール |

**古いフォルダの一覧**:

移行後に削除される古いフォルダは次のとおりです。

>[!NOTE]
>
>古いフォルダのコンテンツ全体を確認し、各品目に対して、コンサルタントがその内容を保持するか削除するかを決定します。 保管する物は適所へ移すべし

| 内部名 | ラベル | 条件 |
|---|---|---|
| nmsAdministration | 管理 | - |
| nmsDeliveryMgt | キャンペーンの実行 | - |
| ncmContent | コンテンツ管理 | Content Managerがインストールされました |
| ncmForm | 入力フォーム | Content Managerがインストールされました |
| ncmImage | 画像 | Content Managerがインストールされました |
| ncmJavascript | JavaScript コード | Content Managerがインストールされました |
| ncmJst | JavaScript テンプレート | Content Managerがインストールされました |
| ncmParameters | 設定 | Content Managerがインストールされました |
| ncmSrcSchema | データスキーマ | Content Managerがインストールされました |
| ncmStylesheet | XSLスタイルファイル | Content Managerがインストールされました |
| nmsAdminPlan | 管理 | キャンペーンのインストール |
| nmsResourcePlan | リソース | キャンペーンのインストール |
| nmsResourcesModels | テンプレート | キャンペーンのインストール |
| nmsRootPlan | キャンペーン管理 | キャンペーンのインストール |
| nmsOperator | マーケティング業者 | MRMがインストールされました |

