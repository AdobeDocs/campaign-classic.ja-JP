---
title: '"ユースケース：Web フォーム"'
seo-title: '"ユースケース：Web フォーム"'
description: '"ユースケース：Web フォーム"'
seo-description: null
page-status-flag: never-activated
uuid: b2c3f171-325e-4913-a188-a791bad0df2e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-forms
discoiquuid: cfa22577-0b9e-4eee-900d-214b81256d81
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c9c9d5f96856ce9e19571bad032d2bf04eaa60bd

---


# ユースケース：Web フォーム{#use-cases-web-forms}

## 二重のオプトインを備えた購読フォームの作成 {#create-a-subscription--form-with-double-opt-in}

情報サービスを提供する場合、受信者は、リンクされたすべての通信を受信するために購読する必要があります。不適切な通信を避け、受信者が意図的に購読したことを確認するために、購読の確認リクエストを送信して、二重のオプトインを作成することをお勧めします。確認メッセージに含まれるリンクをユーザーがクリックした場合にのみ、購読が有効になります。

この例は、次のシナリオに基づいています。

1. 一時的なサービスを購読するためのチェックボックスが含まれた、Web サイト上のニュースレターの購読フォームの作成。このサービスにより、購読確認メッセージを配信できます。
1. Web フォームにリンクされた配信テンプレートを使用した、購読確認配信の作成。これには確認リンクが含まれています。この確認リンクは、ニュースレター購読用のフォームを呼び出して、購読承認メッセージを表示します。

### 手順 1 - 情報サービスの作成 {#step-1---creating-information-services}

1. 受信者に提供されるニュースレター購読サービスを作成します。ニュースレターの作成方法について詳しくは、[この節](../../delivery/using/about-services-and-subscriptions.md)を参照してください。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_1.png)

1. 2 番目の情報サービスとして、購読確認メッセージを送信するための配信テンプレートにリンクされた一時的なサービスを作成します。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_1c.png)

### 手順 2 - 確認メッセージの作成 {#step-2---creating-confirmation-messages}

確認メッセージは、一時的なサービスレベルで参照される専用の配信テンプレートを使用して送信されます。

1. で、を選 **[!UICONTROL Explorer]** 択します **[!UICONTROL Resources > Templates > Delivery templates]**。
1. 購読確認メッセージを送信するための配信テンプレートを作成します。
1. Click the **[!UICONTROL To]** button in the **[!UICONTROL Email parameters]** to associate the delivery template with the Subscriptions target mapping instead of Recipients.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_1d.png)

1. この配信の受信者は、承認を確認していないので、まだデータベースでブラックリストに登録されています。この通信を受信するには、このテンプレートに基づいて配信を承認して、ブラックリストに登録された受信者をターゲットにする必要があります。

   To do this, click the **[!UICONTROL Exclusions]** tab.

1. リンクをクリックし **[!UICONTROL Edit...]** て、このオプションのチェックを **[!UICONTROL Exclude recipients who no longer want to be contacted (blacklist)]** 外します。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_4d.png)

   >[!CAUTION]
   >
   >このオプションは、このタイプのコンテキストでのみ無効にできます。

1. 配信をパーソナライズし、確認リンクをメッセージコンテンツに挿入します。このリンクをクリックすると、購読確認を記録する Web フォームにアクセスできます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_1b.png)

1. DCE で URL を Web フォームにリンクします。Web フォームはまだ作成していないので、作成したらすぐに値を置き換えます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_3.png)

1. 最後に、先ほど作成した一時的なサービスにこのテンプレートをリンクします。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_3c.png)

### 手順 3 - 購読フォームの作成 {#step-3---creating-the-subscription-form}

Web フォームでは、受信者の購読と購読確認の両方が可能です。

Web フォームのワークフローには、次のアクティビティが含まれます。

![](assets/s_ncs_admin_survey_double-opt-in_sample_4c.png)

これをおこなうには、以下の手順に従います。

1. Webフォームを作成し、テンプレートを選択しま **[!UICONTROL Newsletter subscription (subNewsletter)]**&#x200B;す。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_5a.png)

1. In the **[!UICONTROL Edit]** tab, we need to configure the existing workflow since we want to add a confirmation message to the recipients who want to subscribe.

   To do so, double-click the **[!UICONTROL Preloading]** box and configure it as follows.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_5b.png)

   これは、ユーザーが確認メッセージのリンクを使用してこのフォームにアクセスする場合、ユーザーのプロファイル情報が読み込まれることを意味します。Web サイトのページを使用して Web フォームにアクセスする場合、情報は読み込まれません。

1. Add a **[!UICONTROL Test]** activity to your workflow.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_6e.png)

   The **[!UICONTROL Test]** activity can concern the recipient email. ここでは、次のように設定します。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_6d.png)

1. Add two **[!UICONTROL Script]** activities to your workflow.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_6f.png)

   The first **[!UICONTROL Script]** activity will blacklist recipients until they confirmed their subscription to the newsletter. このアクティビティの内容は、次のようにする必要があります。

   ```
   ctx.recipient.@blackList=1
   ```

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_6bbis.png)

   The second **[!UICONTROL Script]** activity authorizes deliveries to be send to the users and subscribes them to the newsletter. スクリプトの最後の 2 行を使用して、受信者を一時フォルダーから別のフォルダーに転送できます。また、これらの行は、受信者が購読を確認するとすぐに既存のプロファイルと紐付けられます。

   ```
   ctx.recipient.@blackList=0
   nms.subscription.Subscribe("INTERNAL_NAME_OF_THE_NEWSLETTER", ctx.recipient, false)
   ctx.recipient.folder = <folder name="nmsRootRecipient"/>
   nms.subscription.Unsubscribe("TEMP", ctx.recipient)
   ```

   >[!NOTE]
   >
   >**[!UICONTROL Temp]** パーティションは、ワークフローを使用して定期的にパージすることもできます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_6b.png)

1. Double-click the **[!UICONTROL Subscription]** activity to personalize the subscription form and link a checkbox with the temporary service previously created.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_5c.png)

1. Configure the **[!UICONTROL Storage]** activity to save the information entered in the form page.

   このアクティビティを使用すると、専用の一時的な受信者プロファイルを、データベースのプロファイルとは別に作成し、一時的な受信者プロファイルにメッセージを送信できます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_5g.png)

   >[!NOTE]
   >
   >紐付けオプションを定義しないようにする必要があります。

1. Add two **[!UICONTROL End]** activities to display a message for the user.

   The second **[!UICONTROL End]** box will display the confirmation message once the subscription is complete.

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_5h.png)

1. Web フォームを作成し、設定すると、確認メッセージを送信するための配信テンプレートで参照できるようになります。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_7b.png)

### 手順 4 - フォームのパブリッシュとテスト {#step-4---publishing-and-testing-the-form}

これで、ユーザーがアクセスできるようにフォームをパブリッシュできます。

![](assets/s_ncs_admin_survey_double-opt-in_sample_8b.png)

ニュースレターの購読には、次の手順が含まれます。

1. Web サイトのユーザーは、購読ページにログオンし、フォームを承認します。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_8c.png)

   ブラウザーのメッセージで、リクエストを受け付けたことが通知されます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_8d.png)

   ユーザーは、Adobe Campaign データベースの **[!UICONTROL Temp]** フォルダーに追加され、プロファイルがブラックリストに登録されます。この登録は、ユーザーが E メールによる購読確認を完了するまで続きます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_8f.png)

1. 購読を承認するためのリンクに含まれる確認メッセージがユーザーに送信されます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_8e.png)

1. ユーザーがこのリンクをクリックすると、承認ページがブラウザーに表示されます。

   ![](assets/s_ncs_admin_survey_double-opt-in_sample_8.png)

   Adobe Campaign では、ユーザープロファイルが更新されます。

   * ユーザーがブラックリストの登録から除外され、
   * 情報サービスの購読が登録されます。

      ![](assets/s_ncs_admin_survey_double-opt-in_sample_9.png)

## 選択した値に応じた異なるオプションの表示 {#displaying-different-options-depending-on-the-selected-values}

次の例では、ユーザーは自動車のタイプを選択するよう求められます。選択したタイプに応じて、利用可能な自動車のカテゴリを表示できます。つまり、ユーザーの選択によって、右側に表示される項目が変わることを意味します。

![](assets/s_ncs_admin_survey_condition_sample0.png)

* ユーザーが「自家用車」を選択すると、「コンパクト」から「ミニバン」の選択肢が提供されます。

   ![](assets/s_ncs_admin_survey_condition_sample2.png)

* ユーザーが「商用車」を選択すると、選択肢がドロップダウンリストで表示されます。

   ![](assets/s_ncs_admin_survey_condition_sample1.png)

この例では、車両のタイプはデータベースに格納されていません。ドロップダウンリストは次のように設定されます。

![](assets/s_ncs_admin_survey_condition_config1.png)

この情報は、ローカル変数に格納されます。

右側の列の条件付き表示は、コンテナで設定されます。

![](assets/s_ncs_admin_survey_condition_config1bis.png)

* 自家用車用のフィールドの条件付き表示：

   ![](assets/s_ncs_admin_survey_condition_config2.png)

* 商用車用のフィールドの条件付き表示：

   ![](assets/s_ncs_admin_survey_condition_config3.png)

