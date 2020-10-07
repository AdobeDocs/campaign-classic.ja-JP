---
title: v5.11 特有の設定
seo-title: v5.11 特有の設定
description: v5.11 特有の設定
seo-description: null
page-status-flag: never-activated
uuid: d6920beb-a766-4aec-8a8e-d32e47b545a4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: configuration
discoiquuid: fc280640-528d-44de-87d8-52f443772abd
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 5%

---


# v5.11 特有の設定{#specific-configurations-in-v5-11}

この節では、v5.11から移行する際に必要となる追加設定について説明します。 [一般設定](../../migration/using/general-configurations.md) 節で詳しく説明している設定も行う必要があります。

## Web アプリケーション {#web-applications}

移行中、次の警告が自動的に表示されます。

```
The webApp ids have been modified during the migration process. Please make sure to check your scripts/css for broken compatibility (any client side javascript or css dealing directly with another element through its id is impacted). See file 'c:\svn\602\nl\build\ncs\var\upgrade/postupgrade/webAppsMigration_*************.txt' for details about the references that were automatically updated, if any.
```

様々な数式フィールドなど、Webアプリケーションの一部のコンポーネントには、@id属性があります。 これらはWebアプリケーションのXMLコードで使用され、同じ方法では生成されなくなりました。 インターフェイスには表示されず、通常は使用しないでください。 ただし、@id属性を使用してWebアプリケーションのレンダリングをパーソナライズした場合（スタイルシートやJavaScriptコードを使用する場合など）もあります。

移行中に、警告で指定されたログファイルのパスを **確認する必要があります** 。

* **ファイルが空ではありません**:移行前に記録された不一致に関する警告と、現在も存在する警告が含まれます。 これは、存在しないIDを参照するWebアプリケーション内のJavaScriptコードにすることができます。 各エラーをチェックして修正する必要があります。
* **ファイルが空です**:これは、Adobe Campaignが問題を検出していないことを意味します。

ファイルが空かどうかにかかわらず、これらのIDが他の場所での設定に使用されていないことを確認する必要があります（その場合は設定を調整します）。

## ワークフロー {#workflows}

Adobe Campaignのインストールディレクトリの名前が変更されているので、移行後に一部のワークフローが動作しない場合があります。 ワークフローがそのアクティビティの1つでnl5ディレクトリを参照する場合、エラーが発生します。 この参照を **buildに置き換えます**。 SQLクエリを実行して、これらのワークフローを識別できます（PostgreSQLの例）。

```
SELECT   iWorkflowId, sInternalName, sLabel 
FROM XtkWorkflow 
WHERE mData LIKE '%nl5%';
```

## 使いやすさ {#user-friendliness}

Adobe Campaignv5.11のホームページは使用できなくなります。

お勧めしませんが、Adobe Campaignv5.11から特定のインターフェイスを維持したい場合は、いくつかの解決策があります。詳細については、お問い合わせください。

## MySQL {#mysql}

>[!IMPORTANT]
>
>MySQLは、バージョン6.02または5.11からこのエンジンを使用して移行する場合に、v7でメインデータベースエンジンとしてのみサポートされます。

MySQLは、デフォルトでタイムゾーンを管理しません。 タイムゾーン管理を有効にするには、次のコマンドを実行します。

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root mysql
```

>[!NOTE]
>
>詳しくは、https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html [ページを参照してください](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html) 。

データベース構造に変更が加えられた場合は、設定(特定のインデックスの作成、SQL表示の作成など)中に、移行時に一定の予防策を講じる必要があります。 実際、移行手順との互換性のない影響で、一部の変更が生じる可能性があります。 例えば、 **Timestamp** フィールドを含むSQL表示の作成は、 **usetimestamptz** オプションとは互換性がありません。 したがって、以下の推奨事項に従うことをお勧めします。

1. 移行を開始する前に、データベースをバックアップします。
1. SQLの変更を削除します。
1. Adobe Campaign7への移行の [前提条件の節に説明されている手順に従って、アップグレード後にアップグレードを実行します](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 。
   >[!NOTE]
   >
   >Adobe Campaign7への移行の [前提条件の節に示す移行手順に従う必要があります](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 。
1. SQLの変更を再統合します。

この例では、NmcTrackingLogMessages **表示が作成され、** tslogという名前の **Timestamp** フィールドがあり ****&#x200B;ます。 この場合、移行手順は失敗し、次のエラーメッセージが表示されます。

```
2011-10-04 11:57:51.804Z B67B28C0 1 info log Updating table 'NmcTrackingLogMessages'
2011-10-04 11:57:51.804Z B67B28C0 1 error log PostgreSQL error: ERROR: cannot alter type of a column used by a view or rule\nDETAIL: rule _RETURN on view nmctrackinglogmessagesview depends on column "tslog"\n (iRc=-2006)
2011-10-04 11:57:51.804Z B67B28C0 1 error log SQL order 'ALTER TABLE NmcTrackingLogMessages ALTER COLUMN tsLog TYPE TIMESTAMPTZ' was not executed. (iRc=-2006)
```

アップグレード後の動作を確実にするには、移行前に表示を削除し、移行後にTIMESTAMP WITH TIMEZONEモードに適応させて再作成する必要があります。

## トラッキング {#tracking}

トラッキングの数式が変更されました。 移行時に、古い数式(v5)が新しい数式(v7)に置き換えられます。 Adobe Campaignv5でパーソナライズされた数式を使用する場合、この設定はAdobe Campaignv7(**NmsTracking_ClickFormula** および **NmsTracking_OpenFormula** options)で適合する必要があります。

Web トラッキング管理も変更されました。 v7への移行が完了したら、デプロイメントウィザードを開始してWeb追跡の設定を完了する必要があります。

![](assets/migration_web_tracking.png)

次の 3 つのモードを選択できます。

* **セッションWeb追跡**:Leads **** パッケージがインストールされていない場合、このオプションはデフォルトで選択されています。 このオプションは、パフォーマンスの点で最も理想的で、トラッキングログのサイズを制限できます。
* **永久Web トラッキング**
* **匿名Web トラッキング**:Leads **** パッケージがインストールされている場合、このオプションはデフォルトで選択されています。 リソースを最も消費するオプションです。 上記のように、 **sSourceId** 列のインデックスは、(追跡テーブルとCrmIncomingLead **テーブル内で** )作成する必要があります。

>[!NOTE]
>
>For more information on these three modes, refer to [this section](../../configuration/using/about-web-tracking.md).

## Adobe Campaignv7のツリー構造 {#campaign-vseven-tree-structure}

移行中、ツリー構造はv7標準に基づいて自動的に再編成されます。 新しいフォルダが追加され、古いフォルダが削除され、その内容が[移動先]フォルダに配置されます。 このフォルダー内のすべての項目は、移行後にチェックする必要があります。コンサルタントは、このフォルダーを保持するか、各項目を削除するかを決定する必要があります。 保管するアイテムは、適切な場所に移動する必要があります。

ナビゲーションツリーの自動移行を無効にするオプションが追加されました。 この操作は現在手動です。 古いフォルダーは削除されず、新しいフォルダーは追加されません。 このオプションは、標準搭載のv5ナビゲーションツリーが変更を多く受け過ぎた場合にのみ使用してください。 移行前に、 **[!UICONTROL 管理/追加オプション]** ノードで、コンソールに対するオプションを指定します。

* 内部名：NlMigration_KeepFolderStructure
* データタイプ：整数
* 値（テキスト）:1

このオプションを使用する場合、移行後に古いフォルダを削除する必要があります。新しいフォルダを追加し、必要なチェックをすべて実行します。

**新しいフォルダーのリスト**:

移行後、次のフォルダーを追加する必要があります。

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

**古いフォルダーのリスト**:

移行後に削除される古いフォルダーは次のとおりです。

>[!NOTE]
>
>古いフォルダーの内容全体をチェックする必要があり、項目ごとにコンサルタントがその内容を保持するか削除するかを決定します。 保管する物は適当な場所に移動する必要がある。

| 内部名 | ラベル | 条件 |
|---|---|---|
| nmsAdministration | 管理 | - |
| nmsDeliveryMgt | キャンペーンの実行 | - |
| ncmContent | コンテンツ管理 | Content Managerがインストールされました |
| ncmForm | 入力フォーム | Content Managerがインストールされました |
| ncmImage | 画像 | Content Managerがインストールされました |
| ncmJavascript | JavaScript コード | Content Managerがインストールされました |
| ncmJstm | JavaScript テンプレート | Content Managerがインストールされました |
| ncmParameters | 設定 | Content Managerがインストールされました |
| ncmSrcSchema | データスキーマ | Content Managerがインストールされました |
| ncmStylesheet | XSLスタイルファイル | Content Managerがインストールされました |
| nmsAdminPlan | 管理 | キャンペーンのインストール |
| nmsResourcePlan | リソース | キャンペーンのインストール |
| nmsResourcesModels | テンプレート | キャンペーンのインストール |
| nmsRootPlan | キャンペーン管理 | キャンペーンのインストール |
| nmsOperator | マーケティング業者 | MRMがインストールされました |

