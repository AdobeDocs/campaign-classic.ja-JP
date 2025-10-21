---
product: campaign
title: Adobe Campaign ワークスペース
description: Campaign ワークスペースの使用方法とカスタマイズ方法を説明します。
feature: Overview
role: Data Engineer
level: Beginner
exl-id: 5f689679-7148-4abd-a9bf-185854c64b13
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 98%

---

# Adobe Campaign ワークスペース {#adobe-campaign-workspace}

## Adobe Campaign インターフェイスの詳細 {#about-adobe-campaign-interface}

データベースに接続したら、Adobe Campaign のホームページにアクセスします。このページはダッシュボードです。インストールや一般的なプラットフォーム設定に応じて、各機能にアクセスできるリンクとショートカットで構成されています。

ホームページの中心セクションから、リンクを使用して、Campaign のドキュメントポータル、コミュニティおよびアドビカスタマーケア web サイトにアクセスできます。

![](assets/d_ncs_user_interface_home.png)

![](assets/do-not-localize/how-to-video.png) Campaign ワークスペースを[ビデオ](#video)で確認

>[!NOTE]
>
>各インスタンスで利用できる Adobe Campaign 機能は、インストールされているモジュールやアドオンによって異なります。権限や特定の設定によっては、利用できない機能もあります。
>
>モジュールやアドオンをインストールする前に、ライセンス契約を確認する必要があります。詳しくは、アドビのアカウント担当者にお問い合わせください。

### コンソールおよび Web アクセス {#console-and-web-access}

Adobe Campaign プラットフォームにアクセスするには、コンソールまたはインターネットブラウザーを使用します。[互換性マトリックス](../../rn/using/compatibility-matrix.md#Browsers)の互換性のあるブラウザーを確認してください。

Web アクセスインターフェイスは、コンソールインターフェイスに類似しています。ブラウザーからは、コンソールと同じナビゲーションおよび表示機能を使用できますが、キャンペーンに対して実行できるアクションは限られています。 例えば、キャンペーンの表示とキャンセルはできますが、キャンペーンを変更することはできません。任意のオペレーターに対して、キャンペーンは次のようなオプションでコンソールに表示されます。

![キャンペーンのダッシュボードから、キャンペーンの表示やキャンセルができるだけではなく、キャンペーンを変更したり、キャンペーンに配信、ドキュメント、タスクを追加したりできます。](assets/operation_from_console.png)

一方、web アクセスの場合は、次のようなオプションが表示されます。

![ブラウザーでは、同じオペレーターがキャンペーンの表示とキャンセルのみ行うことができます。](assets/operation_from_web.png)

Web インターフェイスの使用について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-create.html?lang=ja#use-the-web-interface-){target=_blank} を参照してください。

### 言語 {#languages}

言語は、Adobe Campaign Classic インスタンスをインストールする際に選択されます。

![](assets/language.png)

次の言語から選択できます。

* 英語（英国）
* 英語（米国）
* フランス語
* ドイツ語
* 日本語

Adobe Campaign Classic インスタンスに選択した言語は、日時フォーマットに影響を与える可能性があります。詳しくは、[Campaign v8（コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank}を参照してください。

インスタンスの作成方法の詳細については、この[ページ](../../installation/using/creating-an-instance-and-logging-on.md)を参照してください。

>[!CAUTION]
>
>インスタンスの作成後は、言語を変更できません。

## ナビゲーションの基本 {#navigation-basics}

### ページの閲覧 {#browsing-pages}

プラットフォームの様々な機能は、いくつかのコア機能に分類されています。インターフェイスの上部のセクションに表示されるリンクを使用して、これらの機能にアクセスします。

![](assets/overview_home.png)

どのコア機能にアクセスできるかは、インストールしたパッケージおよびアドオンと、アクセス権によって異なります。

各コア機能には、タスク関連のニーズと使用コンテキストに基づく一連の機能が含まれています。例えば、「**[!UICONTROL プロファイルとターゲット]**」リンクをクリックすると、受信者リスト、購読サービス、既存のターゲティングワークフローおよびこれらの要素を作成するためのショートカットにアクセスできます。

リストは、「**[!UICONTROL プロファイルとターゲット]**」インターフェイスの左側のセクションにある「**[!UICONTROL リスト]**」リンクから使用できます。

![](assets/recipient_list_overview.png)

### タブの使用 {#using-tabs}

* コア機能またはリンクをクリックすると、現在のページに替わって、該当するページが表示されます。前のページに戻るには、ツールバーの「**[!UICONTROL 戻る]**」ボタンをクリックします。ホームページに戻るには、「**[!UICONTROL ホーム]**」ボタンをクリックします。

  ![](assets/d_ncs_user_interface_back_home_buttons.png)

* メニューまたは表示画面（Web アプリケーション、プログラム、配信、レポートなど）へのショートカットの場合は、対応するページが別のタブで表示されます。これにより、タブを使用してページからページに移動することができます。

  ![](assets/d_ncs_user_interface_tabs.png)

### 要素の作成 {#creating-an-element}

各コア機能のセクションでは、使用可能な各種の要素を参照できます。そのためには、「**[!UICONTROL ブラウジング]**」セクションのショートカットを使用します。「**[!UICONTROL その他]**」リンクを使用すると、環境に関わらず、その他のすべてのページにアクセスできます。

画面左にある「**[!UICONTROL 作成]**」セクションのショートカットを使用して、新しい要素（配信、Web アプリケーション、ワークフローなど）を作成できます。リストの上にある「**[!UICONTROL 作成]**」ボタンを使用すると、リストに新しい要素を追加できます。

例えば、配信ページでは、「**[!UICONTROL 作成]**」ボタンを使用して新しい配信を作成します。

![](assets/d_ncs_user_interface_tab_add_del.png)


## Adobe Campaign エクスプローラーの使用 {#using-adobe-campaign-explorer}

Adobe Campaign エクスプローラーにアクセスするには、ツールバーアイコンを使用します。これにより、Adobe Campaign のすべての機能、設定画面およびプラットフォーム要素の一部の詳細ビューにアクセスできます。

Adobe Campaign エクスプローラーについて詳しくは、**Campaign v8（コンソール）ドキュメント**&#x200B;の以下のページを参照してください。

* [Campaign ユーザーインターフェイスの概要](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank}

* [Campaign UI 設定](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/configuration/ui-settings){target=_blank}

* [エクスプローラーでのフォルダーと表示の管理](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/configuration/folders-and-views){target=_blank}


## データのフィルタリング {#filters}

データのフィルタリングとは、特定の条件に一致するレコードのみにデータセットを絞り込むプロセスです。その後、このサブセットを、ターゲット設定されたアクション（更新やオーディエンスの作成など）や分析に使用できます。

Campaign を参照すると、データがリストに表示されます。組み込みフィルターを適用すると、強制隔離されたアドレス、ターゲティングされていない受信者、特定の年齢範囲や作成日のレコードなど、定義済みのサブセットにすばやくアクセスできます。さらに、カスタムフィルターを作成し、後で使用するために保存したり、他の Campaign ユーザーと共有したりすることもできます。

**フィルターへのアクセス、デザイン、共有**&#x200B;方法については、[Campaign v8（コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/audience/create-filters){target=_blank}を参照してください。


## リストの操作 {#manage-and-customize-lists}

Campaign クライアントコンソールでは、データはリストに表示されます。これらのリストは、ニーズに合わせて調整できます。例えば、列の追加、データのフィルタリング、レコードのカウント、設定の保存と共有を行うことができます。

**リストの管理とカスタマイズ**&#x200B;の方法については、[Campaign v8（コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/configuration/ui-settings#customize-lists){target=_blank}を参照してください。

## 列挙の管理{#managing-enumerations}

定義済みリスト（項目別リストとも呼ばれます）とは、特定のフィールドに入力するために使用できる値の事前定義済みリストです。 定義済みリストはフィールド値の標準化に役立ち、データ入力の一貫性を高め、クエリを簡素化します。

定義すると、値がドロップダウンリストに表示されます。 値は、直接選択するか、予測入力を使用して入力することができます。予測入力では、一致するエントリを提案して完成させます。一部のフィールドには定義済みリストが含まれており、必要に応じて追加の定義済みリストを作成できます。

**定義済みリストの操作**&#x200B;方法について詳しくは、[Adobe Campaign v8（コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/settings/enumerations){target=_blank}を参照してください。

## チュートリアルビデオ {#video}

このビデオでは、Campaign Classic のワークスペースについて説明します。

>[!VIDEO](https://video.tv.adobe.com/v/35130?quality=12)
