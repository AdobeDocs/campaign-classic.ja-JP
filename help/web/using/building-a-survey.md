---
title: 調査の構築
seo-title: 調査の構築
description: 調査の構築
seo-description: null
page-status-flag: never-activated
uuid: 50d501b9-2b4f-48d1-b394-f7f71c413990
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: online-surveys
discoiquuid: 6850851d-1dbe-44f0-bbff-18dbac2cad9a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# 調査の構築{#building-a-survey}

## 新しい調査の作成 {#creating-a-new-survey}

ここでは、Adobe Campaign を使用した&#x200B;**調査**&#x200B;タイプのフォームのデザインと、利用可能なオプションおよび設定について説明します。Adobe Campaign を使用して、作成した調査をユーザーが利用できるようにし、回答を収集してデータベースにアーカイブします。

Webフォームは、ツリーのノードを介 **[!UICONTROL Resources > Online > Web applications]** してアクセスします。 To create a survey, click the **[!UICONTROL New]** button above the list of applications, or right-click the list and choose **[!UICONTROL New]**.

調査テンプレートを選択します（デフォルトは **[!UICONTROL newSurvey]**）。

![](assets/s_ncs_admin_survey_select_template.png)

フォームのページは、入力ゾーン（テキスト）、選択フィールド（リスト、チェックボックスなど）および静的要素（画像、HTML コンテンツなど）を定義および設定できる、特別なエディターで作成されます。They can be collected in &quot;containers&quot; and laid out according to requirements (see [Adding questions](#adding-questions)).

>[!NOTE]
>
>Web フォームのコンテンツの定義方法および画面レイアウトの作成方法について詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

## フィールドの追加 {#adding-fields}

フォームのフィールドは、ユーザーによる情報の入力とオプションの選択を可能にします。For each page in the form, they are created via the first button in the toolbar using the **[!UICONTROL Add using the wizard]** menu.

![](assets/s_ncs_admin_survey_add_field_menu.png)

>[!NOTE]
>
>右クリックを使用して入力ゾーンを挿入することもできます。デフォルトでは、ゾーンは、選択したツリーの最後に挿入されます。ツールバーの矢印を使用して移動します。

### フィールドのタイプ {#types-of-fields}

調査にフィールドを追加する場合、タイプを選択する必要があります。次のオプションを使用できます。

1. **[!UICONTROL Answer a question]**:このオプションを使用すると、回答を保存する新しいフィールド（「アーカイブ済みフィールド」と呼ばれます）を宣言できます。 この場合、参加者が複数回フォームに入力した場合を含め、収集したすべての値が保存されます。このストレージモードは、**調査**&#x200B;でのみ使用できます。「収集した回答 [の保存」を参照](../../web/using/managing-answers.md#storing-collected-answers)。
1. **[!UICONTROL Edit a recipient]**:このオプションを使用すると、データベース内のフィールドを選択できます。 この場合、ユーザーの回答は、このフィールドに格納されます。各参加者では、保存した最後の値のみが保持され、プロファイルデータに追加されます。
1. **[!UICONTROL Add a variable]**:このオプションを使用すると、情報がデータベースに保存されないように設定を作成できます。 ローカル変数はアップストリームを宣言できます。また、フィールドを作成する際に、直接追加できます。
1. **[!UICONTROL Import an existing question]**:このオプションを使用すると、他の調査で作成された既存の質問をインポートできます。

   >[!NOTE]
   >
   >ストレージモードとフィールドインポートの詳細については、「収集した回 [答の保存」を参照してくださ](../../web/using/managing-answers.md#storing-collected-answers)い。

追加するフィールドの特性（ドロップダウンリスト、テキストフィールド、チェックボックスなど）は、選択したストレージモードに適応されます。You can change it using the **[!UICONTROL Type]** field of the **[!UICONTROL General]** tab, but make sure to remain consistent with the data type.

![](assets/s_ncs_admin_survey_change_type.png)

利用可能なフィールドの様々なタイプについて詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

## 調査に特有の要素 {#survey-specific-elements}

オンライン調査では Web アプリケーションの機能を使用します。ここでは、調査フィールドに特有の機能について説明します。

### 複数選択 {#multiple-choice}

For **[!UICONTROL Multiple choice]** type controls, you can define a minimum and maximum number of selections. 例えば、このオプションを使用すると、利用可能なオプションから、少なくとも **2** つの値、最大でも **4** つの値の選択を強制できます。

![](assets/s_ncs_admin_survey_multichoice_ex1.png)

選択肢の数が多すぎるか少なすぎる場合、適切なメッセージが表示されます。

![](assets/s_ncs_admin_survey_multichoice_ex2.png)

>[!NOTE]
>
>この場合、オプションは、チェックボックスを使用して選択されます。1 つのオプションのみ有効な場合、ラジオボタンが使用されます。

対応する設定は次のようになります。

![](assets/s_ncs_admin_survey_multichoice_ex3.png)

In addition, the storage location for this input field must be a **[!UICONTROL Multiple values]** type **archived field**:

![](assets/s_ncs_admin_survey_multiple_values_field.png)

>[!CAUTION]
>
>* この機能は、**調査**&#x200B;タイプのフォームでのみ使用できます。
>* このオプションは、ランダムな質問の表示とは互換性がありません。For more on this, refer to [Adding questions](#adding-questions).


### 質問の追加 {#adding-questions}

標準および質問の 2 つのタイプのコンテナがあります。標準コンテナは、ページレイアウトおよびページの条件付き表示を設定するために使用されます。詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

**質問**&#x200B;コンテナを使用して、質問をページに追加したり、考えられる回答を階層の下に挿入したりします。このタイプのコンテナに配置された質問に対するユーザーの回答は、レポートで分析できます。

>[!CAUTION]
>
>**質問**&#x200B;コンテナを別の&#x200B;**質問**&#x200B;コンテナの下の階層に挿入しないでください。

![](assets/s_ncs_admin_question_label.png)

質問のラベルは、ラベルフィールドに入力されます。この場合、フォームのスタイルシートからのスタイルが適用されます。パーソナライズする **[!UICONTROL Enter the title in HTML format]** オプションを選択します。 これにより、HTML エディターにアクセスできるようになります。

>[!NOTE]
>
>HTML エディターの使用について詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

次に例を示します。

![](assets/s_ncs_admin_survey_containers_qu_arbo.png)

上記の例では、レンダリングは次のようになります。

![](assets/s_ncs_admin_survey_containers_qu_ex.png)

>[!NOTE]
>
>すべての質問は、**質問**&#x200B;タイプのコンテナを持ちます。

Adobe Campaign による質問のランダムな抽選を有効にできます。次に、設定ウィンドウの下部にあるフィールドに、ページに表示される質問の数を指定します。

![](assets/s_ncs_admin_survey_containers_qu_display.png)

レンダリングは、次のようになります。

![](assets/s_ncs_admin_survey_containers_qu_display_rendering.png)

ページが更新されると、表示される質問は異なります。

>[!CAUTION]
>
>When you display a question randomly (**[!UICONTROL Display randomly]** option checked on the page), be careful not to use multiple choice questions for which one or more selections are mandatory.

