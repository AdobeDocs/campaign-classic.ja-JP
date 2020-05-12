---
title: タイムゾーン管理
seo-title: タイムゾーン管理
description: タイムゾーン管理
seo-description: null
page-status-flag: never-activated
uuid: b8926761-65e2-48fd-8689-2ae6b0596e72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: additional-configurations
discoiquuid: b9846eda-eeca-433e-b961-6dfc2aa2708b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 3522f4f50770dde220610cd5f1c4084292d8f1f5
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 1%

---


# タイムゾーン管理{#time-zone-management}

## 動作の仕組み {#operating-principle}

Adobe Campaignを使用すると、日付をタイムゾーンの関数として表すことができます。 これにより、国際的なユーザーは世界中の様々なタイムゾーンで作業を行うことができます。 同じインスタンスを使用する各国で、キャンペーンの実行、追跡、アーカイブなどを管理できます。 ローカル時間に応じて異なります。

Adobe Campaignプラットフォームの使用を国際的な規模で有効にするには、システムが使用するすべての日付がタイムゾーンにリンク可能である必要があります。 したがって、タイムゾーンが既知の日付は、他のタイムゾーンにインポートすることも、タイムゾーンに関係なくインポートすることもできます。

Adobe Campaignを使用すると、日付/時刻をUTC（協定世界時）形式で格納できます。 データが公開されると、演算子のローカルな日付/時間に変換されます。 変換は、データベースがUTCで設定される場合に自動的に実行されます( [設定](#configuration))。 データベースがUTCで設定されていない場合、プラットフォーム内の日付のタイムゾーンに関する情報は、オプションに格納されます。

タイムゾーン管理に関する主なプラットフォーム機能は次のとおりです。 データおよび演算子とワークフロー管理の読み込み/書き出し。 **継承の概念** は、読み込み/書き出しまたはワークフローで使用できます。 デフォルトでは、これらのタイムゾーンはデータベースサーバーのタイムゾーンに設定されますが、ワークフローや単一のアクティビティに対しても、新しいタイムゾーンを再定義できます。

**演算子** は、 **配信の設定時にタイムゾーンを変更でき** 、配信を実行する特定のタイムゾーンを指定できます。

>[!IMPORTANT]
>
>データベースが複数のタイムゾーンを管理していない場合は、すべてのデータフィルタリング操作に対して、SQLクエリをデータベースサーバーのタイムゾーンで実行する必要があります。

各Adobe Campaign演算子はタイムゾーンにリンクされています。 この情報は、ユーザーのプロファイルで設定されます。 For more on this, refer to [this document](../../platform/using/access-management.md).

Adobe Campaignプラットフォームでタイムゾーン管理が不要な場合は、特定のタイムゾーンを含むストレージモードをローカルフォーマットに保つことができます。

## 推奨事項 {#recommendations}

タイムゾーンには、次のようないくつかの現実が組み合わされています。 式は、UTCの日付と一定の時間差、または年に2回（夏時間）時間が変わる地域の時間を表すことができます。

例えば、postgreSQLでは、 **SET TIME ZONE &#39;Europe/Paris&#39;;** コマンドでは、夏と冬の時間が考慮されます。 日付は、年の時刻に応じてUTC+1またはUTC+2で表されます。

ただし、 **SET TIME ZONE 0200;** のタイムラグは常にUTC+2になります。

## 設定 {#configuration}

日付と時間のストレージモードは、データベースの作成時に選択します(「新しいインスタンスの [作成](#creating-a-new-instance)」を参照)。 移行の場合、日付にリンクされた時間はローカルの日付と時間に変換されます( [移行](#migration))。

技術的な表示点から、 **日付+時間** 型の情報をデータベースに格納する方法は2つあります。

1. TIMESTAMP WITH TIMEZONE FORMAT: データベースエンジンは、日付をUTCで格納します。 開かれた各セッションにはタイムゾーンが設定され、それに従って日付が変換されます。
1. ローカル形式+ローカルタイムゾーン： すべての日付がローカル形式（タイムラグ管理なし）で保存され、それらに単一のタイムゾーンが割り当てられます。 タイムゾーンは、Adobe Campaignインスタンスの **WdbcTimeZone** オプションに格納され、ツリーの **[!UICONTROL 管理/プラットフォーム/オプション]** メニューで変更できます。

>[!IMPORTANT]
>
>この変更により、データの一貫性と同期の問題が発生する可能性があることに注意してください。

### Creating a new instance {#creating-a-new-instance}

複数の国際ユーザーが同じインスタンスで作業できるようにするには、国間の時間差を管理するインスタンスを作成する際に、タイムゾーンを設定する必要があります。 インスタンスの作成時に、データベース設定段階の「 **[!UICONTROL Time zone]** 」セクションで日付と時刻の管理モードを選択します。

日付と時刻をUTC形式で格納する場合は、 **[!UICONTROL UTCデータベース（タイムゾーンを持つ日付フィールド）]** （SQLフィールドおよびXMLフィールド）オプションをオンにします。

![](assets/install_wz_select_utc_option.png)

>[!IMPORTANT]
>
>Oracle ****&#x200B;を使用している場合は、Oracleクライアント層のタイムゾーンファイル(.dat)が、サーバーにインストールされているタイムゾーンファイルと互換性がある必要があります。

データベースがUTCでない場合は、ドロップダウンリストで提供されるタイムゾーンの1つを選択できます。 サーバーのタイムゾーンを使用することも、「UTC（協定世界時）」オプションを選択することもできます。

![](assets/install_wz_unselect_utc_option.png)

「 **[!UICONTROL UTC Database（タイムゾーンのある日付フィールド）]** 」オプションが選択されている場合、SQLフィールドはTIMESTAMP WITH TIMEZONE形式で保存されます。

それ以外の場合は、ローカル形式で保存されるので、データベースに適用するタイムゾーンを選択する必要があります。

### Migration {#migration}

タイムゾーン管理を使用せずに以前のバージョンに移行する場合は、データベースで日付ストレージモードを定義する必要があります。

Adobe Campaignデータベースにアクセスする外部ツールとの互換性を保証するため、 **Date+time** 型のSQLフィールドは、デフォルトでローカル形式で保存されたままになります。

日付を含むXMLフィールドは、現在はUTCで保存されます。 読み込み中、UTC形式ではないフィールドは、サーバーのタイムゾーンを使用して自動的に変換されます。 つまり、すべてのXMLフィールドは、UTC形式にプログレッシブに変換されます。

既存のインスタンスを使用するには、 **WdbcTimeZone** オプションを追加し、インスタンスのタイムゾーンを入力します。

>[!IMPORTANT]
>
>WdbcTimeZoneオプションに正しい値が構成されていることを確認してください： 後で行う変更は、矛盾を引き起こす可能性がある。

可能な値の例：

* Europe/Paris,
* Europe/London,
* America/New_Yorkなど

   これらの値は、tz(Olson)データベースから取得されます。 詳しくは、https://en.wikipedia.org/wiki/List_of_tz_database_time_zonesを参照してくだ [さい](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。

