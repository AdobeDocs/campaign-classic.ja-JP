---
title: マーケティングキャンペーンへのアクセス
seo-title: マーケティングキャンペーンへのアクセス
description: マーケティングキャンペーンへのアクセス
seo-description: null
page-status-flag: never-activated
uuid: a482be37-61bb-4588-9dfb-f9c3ee5a1930
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: campaign
content-type: reference
topic-tags: about-marketing-campaigns
discoiquuid: 8e7eb53c-bbe2-4bd4-8581-c2a63a3dc84e
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: b47dcfa0e4ee2e5e43e7aa14b94e12fd70ff9c2d

---


# マーケティングキャンペーンへのアクセス{#accessing-marketing-campaigns}

Adobe Campaign では、マーケティングキャンペーンを作成、設定、実行および分析できます。すべてのマーケティングキャンペーンを統合コントロールセンターから管理できます。

## ワークスペースの基本 {#workspace-basics}

### ホームページ {#home-page}

Adobe Campaign に接続すると、ホームページが表示されます。

![](assets/campaign_global_view.png)

各種ウィンドウにアクセスするには、ナビゲーションバーのリンクをクリックします。

**[!UICONTROL キャンペーン]**&#x200B;ウィンドウにはキャンペーンの様々な要素があります。ここでは、マーケティングプログラムおよびキャンペーン、そのサブセットの概要について説明します。マーケティングプログラムは複数のキャンペーンで構成され、キャンペーンは配信、タスク、リンクされたリソースなどで構成されます。キャンペーンを使用したマーケティングキャンペーン管理のコンテキストでは、配信、予算、レビュー担当者およびリンクされたドキュメントに関する情報がキャンペーンに含まれます。

**[!UICONTROL キャンペーン]**&#x200B;ウィンドウのナビゲーションブロックには、インスタンス上にインストールされているモジュールに応じて様々なエントリがあります。例えば、以下にアクセスできます。

* **キャンペーンカレンダー**：プラン、マーケティングプログラム、配信およびキャンペーンのカレンダーです。[キャンペーンカレンダー](#campaign-calendar)を参照してください。
* **キャンペーン**：すべてのマーケティングプログラムに含まれるキャンペーンにアクセスします。
* **配信**：キャンペーンにリンクされた配信にアクセスします。
* **Web アプリケーション**：Web アプリケーション（フォーム、調査など）にアクセスします。

>[!NOTE]
>
>Adobe Campaign 全体のエルゴノミクス、権限およびプロファイル管理機能については、[この節](../../platform/using/adobe-campaign-workspace.md)を参照してください。
>
>チャネルおよび配信に関連するすべての機能については、[この節](../../delivery/using/communication-channels.md)で詳しく説明しています。

### キャンペーンカレンダー {#campaign-calendar}

各キャンペーンはプログラムに所属し、プログラムはプランに所属します。プラン、プログラムおよびキャンペーンには、**キャンペーン**&#x200B;ウィンドウの&#x200B;**[!UICONTROL キャンペーンカレンダー]**&#x200B;メニューからアクセスします。

プラン、プログラム、キャンペーンまたは配信を編集するには、カレンダー内でその名前をクリックし、「**[!UICONTROL 開く...]**」をクリックします。すると、次のように新しいタブに表示されます。

![](assets/d_ncs_user_interface_hierar.png)

キャンペーンカレンダーに表示する情報をフィルタリングできます。フィルタリングするには、「**[!UICONTROL フィルター]**」リンクをクリックして、フィルタリング条件を選択します。

![](assets/campaign_planning_filter.png)

>[!NOTE]
>
>日付に対してフィルターを設定すると、開始日が指定された日付以降または終了日が指定された日付以前のキャンペーンがすべて表示されます。日付は、各フィールドの右側のカレンダーを使用して選択する必要があります。

「**[!UICONTROL 検索]**」フィールドを使用して、表示する項目をフィルタリングすることもできます。

各項目にリンクされたアイコンを使用して、「完了」、「処理中」、「編集中」などのステータスを表示できます。

### マーケティングプログラムの参照 {#browsing-in-a-marketing-program}

キャンペーンでは、様々なマーケティングキャンペーンで構成された一連のプログラムを管理できます。各キャンペーンには、配信および関連するプロセスとリソースが含まれます。

#### プログラムの参照 {#browsing-a-program}

プログラムを編集する際は、後述のタブを使用して、プログラムを参照および設定します。

* 「**スケジュール**」タブには、カレンダーのヘッダーでクリックしたタブに応じて、1 ヶ月、1 週間または 1 日のプログラムのカレンダーが表示されます。

   必要に応じて、このページからキャンペーン、プログラムまたはタスクを作成できます。

   ![](assets/s_ncs_user_interface_campaign02.png)

* 「**編集**」タブを使用して、名前、開始日と終了日、予算、リンクされたドキュメントなど、プログラムをパーソナライズできます。

   ![](assets/s_ncs_user_interface_campaign05.png)

#### キャンペーンの参照 {#browsing-campaigns}

キャンペーンには、キャンペーンカレンダー、プログラムの「**[!UICONTROL スケジュール]**」タブ、キャンペーンのリストからアクセスできます。

1. キャンペーンカレンダーからは、表示したいキャンペーンを選択し、「**[!UICONTROL 開く]**」リンクをクリックします。

   ![](assets/campaign_planning_edit_op.png)

   次のように、キャンペーンは新しいタブで編集されます。

   ![](assets/campaign_op_edit.png)

1. プログラムの「**[!UICONTROL スケジュール]**」タブからアクセスする場合、編集モードはキャンペーンカレンダーからアクセスする場合と同じです。
1. **[!UICONTROL キャンペーン]**&#x200B;ウィンドウの「**[!UICONTROL キャンペーン]**」リンクから、編集したいキャンペーンの名前をクリックします。

   ![](assets/campaign_edit_from_list.png)

### キャンペーンのコントロール {#controlling-a-campaign}

#### ダッシュボード {#dashboard}

キャンペーンごとに、ジョブ、リソース、配信を単一の画面、すなわちダッシュボードで一元管理します。ダッシュボードを使用すると、他のユーザーと協調してマーケティングアクションを管理できます。

キャンペーンのダッシュボードをコントロールインターフェイスとして使用します。ダッシュボードから、配信、抽出ファイル、通知、予算など、メインのキャンペーン作成および管理ステージに直接アクセスできます。

![](assets/s_ncs_user_op_board_start_del.png)

Adobe Campaign では、予算、ターゲット、コンテンツなどを承認する、マーケティングおよびコミュニケーションキャンペーンの様々なステージの作成および承認のための協調プロセスを設定できます。

![](assets/s_ncs_user_op_board_validate.png)

>[!NOTE]
>
>キャンペーンテンプレートの設定について詳しくは、[キャンペーンテンプレート](../../campaign/using/marketing-campaign-templates.md#campaign-templates)で説明しています。

#### スケジュール {#schedule}

キャンペーンは、一連の配信を一元管理します。スケジュールでは、キャンペーンごとのすべてのコンポーネントがグローバルビューで表示されます。このビューにタスクと配信を表示し、容易にアクセスすることができます。

![](assets/campaign_planning_tab.png)

#### フォーラム {#forum}

キャンペーンごとに、オペレーターが専用のフォーラムでメッセージをやり取りできます。

詳しくは、[ディスカッションフォーラム](../../campaign/using/discussion-forums.md)を参照してください。

#### レポート {#reports}

「**[!UICONTROL レポート]**」リンクを使用して、キャンペーンレポートにアクセスできます。

![](assets/campaign_reporting_tab.png)

>[!NOTE]
>
>レポートについて詳しくは、[この節](../../reporting/using/about-adobe-campaign-reporting-tools.md)を参照してください。

#### 設定 {#configuration}

キャンペーンは、キャンペーンテンプレートから作成します。一部のオプションが選択され、その他の設定が既に保存されている、再利用可能なテンプレートを設定できます。キャンペーンごとに、次の機能が提供されます。

* ドキュメントとリソースの参照：ドキュメント（概要、レポート、画像など）とキャンペーンを関連付けることができます。あらゆるドキュメントフォーマットをサポートしています。[関連付けられたドキュメントの管理](../../campaign/using/marketing-campaign-deliveries.md#managing-associated-documents)を参照してください。
* コストの定義：Adobe Campaign では、キャンペーンごとに、コストエントリと、マーケティングキャンペーン作成時に使用できるコスト計算構造を定義できます。例えば、印刷コスト、外部エージェンシーの利用、部屋の賃借などがあります。[コストカテゴリの定義](../../campaign/using/providers--stocks-and-budgets.md#defining-cost-categories)を参照してください。
* 目標の定義：購読者数や取引高など、キャンペーンの定量化可能な目標を定義できます。この情報は、後でキャンペーンレポートに使用されます。
* シードアドレス（詳しくは、[この節](../../delivery/using/about-seed-addresses.md)を参照）およびコントロール母集団（[コントロール母集団の定義](../../campaign/using/marketing-campaign-deliveries.md#defining-a-control-group)を参照）の管理。
* 承認の管理：承認を得る処理や、必要に応じてレビュー担当のオペレーターまたはオペレーターのグループを選択できます。[配信の確認と承認](../../campaign/using/marketing-campaign-approval.md#checking-and-approving-deliveries)を参照してください。

>[!NOTE]
>
>キャンペーンの設定にアクセスして変更するには、「**[!UICONTROL 編集]**」タブの「**[!UICONTROL キャンペーンの詳細パラメーター...]**」リンクをクリックします。配信が自動的に値を継承するよう、キャンペーンレベルでパラメーターを設定する方法について詳しくは、[このテクニカルノート](https://helpx.adobe.com/jp/campaign/kb/simplifying-campaign-management-acc.html#Setparametersatthecampaignlevelsodeliveriesinheritvaluesautomatically)を参照してください。

## Web インターフェイスの使用 {#using-the-web-interface-}

インターネットブラウザーから Adobe Campaign のコンソール画面にアクセスして、キャンペーンと配信だけでなく、レポートやデータベース内のプロファイルに関する情報も確認できます。このアクセスでは、レコードは作成できません。オペレーターの権限に応じて、データベース内のデータを確認したり、データに基づいて行動したりできます。例えば、キャンペーンのコンテンツとターゲティングを承認したり、配信を再開または停止することが可能です。

1. https://`<your instance>:<port>/view/home` から通常どおりにログオンします。
1. メニューを使用して概要にアクセスします。

   ![](assets/s_ncs_user_interface_web_campaign_01.png)

（ターゲットや配信コンテンツなどの）承認は、Web アクセスから実行できます。

![](assets/campaign_web_interface_validation.png)

通知メッセージに含まれるリンクを使用することもできます。詳しくは、[配信の確認と承認](../../campaign/using/marketing-campaign-approval.md#checking-and-approving-deliveries)を参照してください。
