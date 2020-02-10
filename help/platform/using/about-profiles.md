---
title: プロファイルについて
seo-title: プロファイルについて
description: プロファイルについて
seo-description: null
page-status-flag: never-activated
uuid: 9a3fcb58-a356-4eee-bc26-c64825de5f99
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: profile-management
discoiquuid: 5addada8-0185-488f-9825-83f60981c139
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0ce6e5277c32bc18c20dca62e5b276f654d1ace5

---


# プロファイルについて{#about-profiles}

## プロファイルのタイプ {#profile-types}

Adobe Campaign では、作成、インポート、ターゲティング、アクショントラッキング、更新など、プロファイルをライフサイクル全体にわたって管理できます。

各プロファイルは、データベースエントリに対応します。これには、個人のターゲティング、選定およびトラッキングに必要な情報がすべて含まれています。

プロファイルは、ストレージスペースに基づいて識別できます。つまり、プロファイルは受信者、訪問者、オペレーター、購読者、見込み客などに対応します。

## 受信者プロファイル {#recipient-profiles}

配信の受信者はプロファイルとしてデータベースに保存されており、これには、姓、名、住所、購読、配信など、受信者に関連付けられた情報が含まれます。キャンペーンを作成する場合、配信のターゲットを、単純な基準または詳細な基準に従って選択されたベース内のプロファイルに定義できます。

プロファイルがデータベースではなくファイルに保存されている受信者を対象にしたキャンペーンを作成することもできます。これらは「外部」配信と呼ばれます。このタイプの配信について詳しくは、[このページ](../../delivery/using/steps-defining-the-target-population.md#selecting-external-recipients)を参照してください。

受信者プロファイルを作成する主な方法は次のとおりです。

* グラフィカルインターフェイス画面での直接入力
* 受信者リストのインポート
* Web フォームによるオンライン収集

>[!NOTE]
>
>To find out how files and web forms are imported, refer to [Generic imports and exports](../../platform/using/generic-imports-and-exports.md).

## プロファイルとターゲット {#profiles-and-targets}

The **[!UICONTROL Profiles and targets]** link lets you display recipients stored in Adobe Campaign database. 新規受信者の作成、既存の受信者の編集およびそのプロファイルへのアクセスをおこなうことができます。詳しくは、[このページ](../../platform/using/editing-a-profile.md)を参照してください。

![](assets/d_ncs_user_interface_target_link.png)

次のものにアクセスすることもできます。

* リスト；詳しく [は、リストの作成と管理](../../platform/using/creating-and-managing-lists.md)、
* 購読サービス：[このページ](../../delivery/using/managing-subscriptions.md)を参照してください。
* Web アプリケーション：[このページ](../../web/using/about-web-applications.md)を参照してください。
* 輸出入（ジョブ）一般的なイ [ンポートとエクスポートを参照](../../platform/using/generic-imports-and-exports.md)。
* ターゲティングワークフロー：[このページ](../../workflow/using/building-a-workflow.md#implementation-steps-)を参照してください。

受信者ページでは、編集、更新、追加、削除、並べ替えなど、頻繁におこなう操作をプロファイルに対して実行できます。

プロファイルをより詳細に操作するには、Adobe Campaign ツリーを編集する必要があります。To do this, click the **[!UICONTROL Explorer]** link on the Adobe Campaign home page.

デフォルトでは、受信者はツリーのノード **[!UICONTROL Profiles and Targets > Recipients]** に保存されます。 このビューでは、受信者の作成のほか、次の操作を実行できます。

* sort and filter the profiles of the database; see [Filtering options](../../platform/using/filtering-options.md),
* move, copy or delete profiles from the database; see [Managing profiles](../../platform/using/managing-profiles.md),
* プロファイルの更新；データ [の更新、](../../platform/using/updating-data.md)
* 受信者のエクスポート；詳しくは、 [プロファイルの書き出しと読み込み](../../platform/using/exporting-and-importing-profiles.md)、
* 受信者グループの作成；詳しくは、 [リストの作成と管理を参照してください](../../platform/using/creating-and-managing-lists.md)。

To access advanced functionalities and configurations, you need to click the **[!UICONTROL Explorer]** icon.

![](assets/d_ncs_user_interface01.png)

Adobe Campaignエクスプローラーの一般的なレイアウトは、「Adobe Campaignエクスプ [ローラーの使用](../../platform/using/adobe-campaign-workspace.md#using-adobe-campaign-explorer)」です。

>[!NOTE]
>
>You can also display an advanced view of this list from the Adobe Campaign tree by clicking the **[!UICONTROL Profiles and targets > Recipients]** link. リスト表示は、ニーズに合わせて設定できます。列の追加または削除、列の順序の定義、データの並べ替えなどを行うことができます。 リスト表示の設定については、Adobe Campaignエクスプ [ローラーの使用を参照してくださ](../../platform/using/adobe-campaign-workspace.md#using-adobe-campaign-explorer)い。
>
>受信者ビューを定義することもできます。この機能の詳細については、「フォルダとビュー」を [参照してください](../../platform/using/access-management.md#folders-and-views)。

## アクティブなプロファイル {#active-profiles}

アクティブなプロファイルは、請求の対象として考慮されるプロファイルです。

「**プロファイル**」とは、エンドユーザー、見込み客またはリードを表している情報のレコード（例：nmsRecipient テーブル内のレコードや、cookie ID、顧客 ID、モバイル ID、または特定のチャネルに関連するその他の情報が含まれている外部テーブル内のレコード）のことです。

請求に関係するのは、**アクティブ**&#x200B;なプロファイルのみです。過去 12 ヶ月以内にいずれかのチャネルでターゲットになるか通信がおこなわれたプロファイルは、アクティブとみなされます。

>[!NOTE]
>
>ただし、Facebook および Twitter チャネルは考慮されません。

の概要は、メニューから確 **[!UICONTROL Number of active profiles]** 認でき **[!UICONTROL Administration > Campaign Management > Customer metrics]** ます。

The actual count is performed by the **[!UICONTROL Number of active billing profiles]** (**[!UICONTROL billingActiveContactCount]**) [technical workflow](../../workflow/using/delivery.md), which runs every day and adds the new data to the existing report for the current period in the **[!UICONTROL Customer metrics]** menu. 各期間は 12 ヶ月続きます。

配信の準備中に（タイポロジルール、強制隔離によって）除外されたプロファイルは、考慮されません。プロファイルは、複数の配信のターゲットになっていても一度しかカウントされません。
