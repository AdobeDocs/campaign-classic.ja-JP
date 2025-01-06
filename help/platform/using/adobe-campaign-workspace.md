---
product: campaign
title: Adobe Campaign ワークスペース
description: Campaign ワークスペースの使用方法とカスタマイズ方法を説明します。
feature: Overview
role: Data Engineer
level: Beginner
exl-id: 5f689679-7148-4abd-a9bf-185854c64b13
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 100%

---

# Adobe Campaign ワークスペース{#adobe-campaign-workspace}



## Adobe Campaign インターフェイスの詳細 {#about-adobe-campaign-interface}

データベースに接続すると、Adobe Campaign ホームページが表示されます。これはダッシュボード形式になっており、各種の機能にアクセスできるリンクとショートカットから構成されています（具体的な内容は、それぞれのインストール構成と一般的なプラットフォーム設定によって異なります）。

ホームページの中心セクションには、Campaign のオンラインドキュメントポータル、フォーラムおよびサポート Web サイトにアクセスするためのリンクが表示されます。

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

[Web インターフェイスの使用](../../campaign/using/accessing-marketing-campaigns.md#using-the-web-interface-)についての詳細情報

### 言語 {#languages}

言語は、Adobe Campaign Classic インスタンスをインストールするときに選択されます。

![](assets/language.png)

次の 5 種類の言語から選択できます。

* 英語（英国）
* 英語（米国）
* フランス語
* ドイツ語
* 日本語

Adobe Campaign Classic インスタンスに選択した言語は、日時フォーマットに影響を与える可能性があります。詳しくは、[この節](../../platform/using/adobe-campaign-workspace.md#date-and-time)を参照してください。

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


## フォーマットと単位 {#formats-and-units}

### 日時 {#date-and-time}

Adobe Campaign Classic インスタンスは、言語によって日時の形式が異なります。

言語は Campaign をインストールする際に選択し、後から変更することはできません。英語（米国）、英語（英国）、フランス語、ドイツ語または日本語を選択できます。詳しくは、[このページ](../../installation/using/creating-an-instance-and-logging-on.md)を参照してください。

米国英語と英国英語の主な違いは次のとおりです。

<table> 
 <thead> 
  <tr> 
   <th> フォーマット<br /> </th> 
   <th> 英語（米国）<br /> </th> 
   <th> 英語（英国）<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 日付<br /> </td> 
   <td> 日曜日が週始め<br /> </td> 
   <td> 月曜日が週始め<br /> </td> 
  </tr> 
  <tr> 
   <td> 日付の短縮表記<br /> </td> 
   <td> <p>%2M/%2D/%4Y</p><p><strong>例：09/25/2018</strong></p> </td> 
   <td> <p>%2D/%2M/%4Y</p><p><strong>例：25/09/2018</strong></p> </td> 
  </tr> 
  <tr> 
   <td> 日付と時刻の短縮表記<br /> </td> 
   <td> <p>%2M/%2D/%4Y %I:%2N:%2S %P</p><p><strong>例：09/25/2018 10:47:25 PM</strong></p> </td> 
   <td> <p>%2D/%2M/%4Y %2H:%2N:%2S</p><p><strong>例：25/09/2018 22:47:25</strong></p> </td> 
  </tr> 
 </tbody> 
</table>

### 列挙への値の追加 {#add-values-in-an-enumeration}

ドロップダウンリストがある入力フィールドを使用して、列挙値を入力できます。この値は、保存してドロップダウンリストのオプションとして提供できます。例えば、受信者プロファイルの「**[!UICONTROL 一般]**」タブの「**[!UICONTROL 市区町村]**」フィールドで、「ロンドン」と入力します。Enter キーを押してこの値を確定すると、この値をフィールドに関連付けられた列挙に対して保存するかどうかを尋ねるメッセージが表示されます。

![](assets/s_ncs_user_wizard_email_bat_substitute_email.png)

「**[!UICONTROL はい]**」をクリックした場合、この値は該当するフィールド（この場合は、**[!UICONTROL ロンドン]**）のコンボボックスで使用可能になります。

>[!NOTE]
>
>列挙（「定義済みリスト」とも呼ばれます）は、管理者が&#x200B;**[!UICONTROL 管理／プラットフォーム／列挙]**&#x200B;セクションで管理します。詳しくは、[列挙の管理](../../platform/using/managing-enumerations.md)を参照してください。

### デフォルトの単位 {#default-units}

有効期間（配信のリソースの有効期間、タスクの承認期限など）を表すフィールドでは、値を次の&#x200B;**単位**&#x200B;で表すことができます。

* **[!UICONTROL s]**（秒）
* **[!UICONTROL mn]**（分）
* **[!UICONTROL h]**（時間）
* **[!UICONTROL d]**（日）

![](assets/enter_unit_sample.png)

## チュートリアルビデオ {#video}

このビデオでは、Campaign Classic のワークスペースについて説明します。

>[!VIDEO](https://video.tv.adobe.com/v/35130?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
