---
product: campaign
title: プロファイルの基本を学ぶ
description: Adobe Campaign でのプロファイルの操作
feature: Profiles, Audiences
role: User, Data Architect
level: Beginner
exl-id: 54f1ad6c-54b0-4448-8c38-806dd75c1dae
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 100%

---

# プロファイルの基本を学ぶ{#about-profiles}



プロファイルは、Adobe Campaign データベースで一元管理されます。 プロファイルを取得してこのデータベースを作成するために使用可能なメカニズムは多数あります。web フォームによるオンライン収集、テキストファイルの手動または自動インポート、会社のデータベースまたは他の情報システムによるレプリケーションなどです。Adobe Campaign を利用すれば、マーケティング履歴、購入情報、嗜好、CRM データおよび関連する PI データを包括的に集約し、分析を行ってアクションに移すことができます。

「**プロファイル**」とは、エンドユーザー、見込み客またはリードを表している情報のレコード（例：nmsRecipient テーブル内のレコードや、cookie ID、顧客 ID、モバイル識別子、または特定のチャネルに関連するその他の情報が含まれている外部テーブル内のレコード）のことです。

Adobe Campaign では、受信者は配信（メール、SMS など）の送信先となるデフォルトプロファイルです。データベースに保存された受信者データを使用すると、特定の配信を受け取るターゲットをフィルタリングしたり、配信コンテンツにパーソナライズデータを追加したりできます。 データベースには、他のタイプのプロファイルも含まれています。それらのプロファイルは用途が異なります。例えば、シードプロファイルは、配信を最終的なターゲットに送信する前のテスト用に作成されます。

![](assets/do-not-localize/how-to-video.png) [ビデオでプロファイルの概念を理解する](#create-profiles-video)

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
* web フォームによるオンライン収集

>[!NOTE]
>
>ファイルおよび web フォームのインポート方法を確認するには、[一般的なインポートおよびエクスポート](../../platform/using/get-started-data-import-export.md)を参照してください。

## プロファイルとターゲット {#profiles-and-targets}

「**[!UICONTROL プロファイルとターゲット]**」リンクをクリックすると、Adobe Campaign データベースに保存されている受信者を表示できます。新規受信者の作成、既存の受信者の編集およびそのプロファイルへのアクセスをおこなうことができます。詳しくは、[このページ](../../platform/using/editing-a-profile.md)を参照してください。

![](assets/d_ncs_user_interface_target_link.png)

次のものにアクセスすることもできます。

* リスト - [詳細情報](../../platform/using/creating-and-managing-lists.md)
* 購読サービス - [詳細情報](../../delivery/using/managing-subscriptions.md)
* web アプリケーション - [詳細情報](../../web/using/about-web-applications.md)
* インポートとエクスポート（ジョブ）- [詳細情報](../../platform/using/about-generic-imports-exports.md)
* ターゲティングワークフロー - [詳細情報](../../workflow/using/building-a-workflow.md#implementation-steps-)

受信者ページでは、編集、更新、追加、削除、並べ替えなど、頻繁におこなう操作をプロファイルに対して実行できます。

プロファイルをより詳細に操作するには、Adobe Campaign ツリーを編集する必要があります。そのためには、Adobe Campaign のホームページで「**[!UICONTROL エクスプローラー]**」リンクをクリックします。

デフォルトでは、受信者はツリーの&#x200B;**[!UICONTROL プロファイルとターゲット／受信者]**&#x200B;ノードに保存されています。このビューでは、受信者の作成のほか、次の操作を実行できます。

* データベースのプロファイルの並べ替えおよびフィルター - [詳細情報](../../platform/using/filtering-options.md)
* データベースからのプロファイルの移動、コピー、削除 - [詳細情報](../../platform/using/managing-profiles.md)
* プロファイルの更新 - [詳細情報](../../platform/using/updating-data.md)
* 受信者のエクスポート - [詳細情報](../../platform/using/exporting-and-importing-profiles.md)
* 受信者グループの作成 - [詳細情報](../../platform/using/creating-and-managing-lists.md)

高度な機能および設定にアクセスするには、「**[!UICONTROL エクスプローラー]**」アイコンをクリックする必要があります。

![](assets/d_ncs_user_interface01.png)

Adobe Campaign エクスプローラーの一般的なレイアウトについては、[このページ](../../platform/using/adobe-campaign-explorer.md)を参照してください。

>[!NOTE]
>
>**[!UICONTROL プロファイルとターゲット／受信者]**&#x200B;リンクをクリックして、Adobe Campaign ツリーからこのリストの詳細ビューを表示することもできます。リスト表示は、ニーズに合わせて設定できます。列の追加または削除、列の順序の定義、データの並べ替えなどをおこなうことができます。リスト表示の設定については、[このページ](../../platform/using/adobe-campaign-ui-lists.md)を参照してください。
>
>受信者ビューを定義することもできます。この機能について詳しくは、[この節](../../platform/using/access-management-folders.md)を参照してください。

## アクティブなプロファイル {#active-profiles}

アクティブなプロファイルは、お客様が過去 12 か月の間に、任意のチャネル経由で通信を試みたプロファイルです。

契約に従い、各キャンペーンインスタンスには、特定数のアクティブなプロファイルがプロビジョニングされ、請求目的でカウントされます。購入したアクティブなプロファイルの数については、最新の契約書を参照してください。詳しくは、[Adobe Campaign 製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}を参照してください。

インスタンスで使用されているアクティブなプロファイル数は、Campaign コントロールパネルから直接監視できます。詳しくは、[コントロールパネルのドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/performance-monitoring/active-profiles-monitoring.html?lang=ja){target="_blank"}を参照してください。

次のガードレールと制限が適用されます。

* 複数の配信のターゲットになっているプロファイルは 1 回だけカウントされます。
* X（Twitter）または Facebook のソーシャルマーケティングのコンテキストでのターゲットプロファイルは、アクティブなプロファイルとして考慮されません。
* アクティブなプロファイルのカウントを使用できるのは、**マーケティングインスタンス**&#x200B;のみです。実行インスタンス、すなわち MID（ミッドソーシング）インスタンスおよび RT（Message Center／リアルタイムメッセージング）インスタンスには使用できません。
* カウントは、受信者のプライマリキーに基づきます。その結果、プロファイルが 2 つの異なる受信者テーブルに存在する場合、アクティブなプロファイルとして 2 回カウントされる可能性があります。


## チュートリアルビデオ {#create-profiles-video}

プロファイルデータにアクセスする方法、プロファイルの並べ替えとフィルターをおこなう方法、プロファイルを手動で作成および管理する方法について説明します。

このビデオでは、Adobe Campaign Classic による一般データ保護規則（GDPR）の遵守についても説明します。

>[!VIDEO](https://video.tv.adobe.com/v/326751?quality=12&captions=jpn)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。

**関連項目：**

* [Campaign のプライバシー管理](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html)

* [ワークフローでのクエリとセグメントデータの作成](../../workflow/using/targeting-data.md)

* [ターゲットマッピングの選択](../../delivery/using/steps-defining-the-target-population.md#select-a-target-mapping)
