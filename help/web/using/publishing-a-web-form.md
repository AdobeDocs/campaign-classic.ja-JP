---
title: Web フォームのパブリッシュ
seo-title: Web フォームのパブリッシュ
description: Web フォームのパブリッシュ
seo-description: null
page-status-flag: never-activated
uuid: 37222829-1d56-438c-a4ca-878925debcb5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-forms
discoiquuid: f4322902-c72d-4443-9c30-09add4c615a3
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# Web フォームのパブリッシュ{#publishing-a-web-form}

## フォームデータのプリロード {#pre-loading-the-form-data}

Web フォームを使用して、データベースに格納されたプロファイルを更新する場合、プリロードボックスを使用できます。プリロードボックスを使用すると、データベースで更新されるレコードの検索方法を示すことができます。

次の識別方法が可能です。

* **[!UICONTROL Adobe Campaign Encryption]**

   この暗号化方法は、暗号化された Adobe Campaign 識別子（ID）を使用します。この方法は、Adobe Campaign オブジェクトにのみ適用でき、暗号化された ID は、Adobe Campaign プラットフォームでのみ生成できます。

   When using this method, you need to adapt the URL of the form to deliver to the email address by adding the **`<%=escapeUrl(recipient.cryptedId) %>`** parameter. 詳しくは、「電子メールでのフォーム [の配信」を参照してください](#delivering-a-form-via-email)。

* **[!UICONTROL DES encryption]**

   ![](assets/s_ncs_admin_survey_preload_methods_001.png)

   この暗号化方法は、外部的に提供される識別子（ID）を使用し、Adobe Campaign および外部プロバイダーによって共有されるキーにリンクされます。The **[!UICONTROL Des key]** field lets you enter this encryption key.

* **[!UICONTROL List of fields]**

   このオプションを使用すると、フォームの現在のコンテキストのフィールドから選択でき、データベースの対応するプロファイルを検索するために使用されます。

   ![](assets/s_ncs_admin_survey_preload_methods_002.png)

   Fields can be added to the form properties via the **[!UICONTROL Parameters]** tab (refer to [Adding parameters](../../web/using/defining-web-forms-properties.md#adding-parameters)). フォーム URL または入力ゾーンに配置されます。

   >[!CAUTION]
   >
   >選択されたフィールドのデータは、暗号化されません。It must not be provided in an encrypted form because Adobe Campaign will not be able to decrypt it if the **[!UICONTROL Field list]** option is selected.

   次の例では、プリロードされるプロファイルは E メールアドレスに基づいています。

   ユーザーが関連するページに直接アクセスできる場合、URL には、暗号化されていない E メールアドレスを含めることができます。

   ![](assets/s_ncs_admin_survey_preload_methods_003.png)

   そうでない場合、パスワードが求められます。

   ![](assets/s_ncs_admin_survey_preload_methods_004.png)

   >[!CAUTION]
   >
   >いくつかのフィールドがリストで指定されている場合、プロファイルをアップロードするために、**すべてのフィールド**&#x200B;のデータがデータベースに格納されたデータと一致する必要があります。そうでない場合、新しいプロファイルが作成されます。
   > 
   >この機能は、Web アプリケーションで特に便利ですが、パブリックフォームにはお勧めしません。選択したアクセス制御オプションは、「アクセス制御を有効にする」が選択されている必要があります。

プロフ **[!UICONTROL Skip preloading if identification is empty]** ァイルを更新しない場合は、このオプションを選択する必要があります。 この場合、入力した各プロファイルは、フォームの承認後にデータベースに追加されます。例えば、フォームが Web サイトに投稿される際に、このオプションが使用されます。

このオ **[!UICONTROL Auto-load data referenced in the form]** プションを使用すると、フォーム内の入力フィールドとマージフィールドに一致するデータを自動的に事前に読み込むことができます。 However, data referenced in **[!UICONTROL Script]** and **[!UICONTROL Test]** activities is not concerned. If this option isn&#39;t selected, you need to define the fields using the **[!UICONTROL Load additional data]** option.

The **[!UICONTROL Load additional data]** option lets you add information which is not used in the pages of the form, but will nonetheless be preloaded.

例えば、受信者の性別をプリロードして、テストボックスを使用して適切なページに自動的に導くことができます。

![](assets/s_ncs_admin_survey_preload_ex.png)

## Web フォームの配信とトラッキングの管理 {#managing-web-forms-delivery-and-tracking}

フォームを作成、設定およびパブリッシュしたら、フォームを配信して回答をトラッキングできます。

### フォームのライフサイクル {#life-cycle-of-a-form}

フォームのライフサイクルには、次の 3 つのステージがあります。

1. **フォーム編集中**

   これは、最初のデザインフェーズです。新しいフォームが作成されると、編集フェーズになります。Access to the form, for testing purposes only, then requires the parameter **[!UICONTROL __uuid]** to be used in its URL. This URL is accessible in the **[!UICONTROL Preview]** sub-tab. フォームURL [パラメーターを参照してくださ](../../web/using/defining-web-forms-properties.md#form-url-parameters)い。

   >[!CAUTION]
   >
   >フォームが編集されている限り、そのアクセス URL は、特別な URL です。

1. **フォームオンライン**

   デザインフェーズが完了すると、フォームは配信できます。最初に、パブリッシュする必要があります。For more on this, refer to [Publishing a form](#publishing-a-form).

   The form will be **[!UICONTROL Live]** until it expires.

   >[!CAUTION]
   >
   >To be delivered, the URL of the survey must not contain the **[!UICONTROL __uuid]** parameter.

1. **フォーム使用不可**

   フォームが閉じられると、配信フェーズが終了し、フォームは使用できなくなり、ユーザーはフォームにアクセスできなくなります。

   期日は、フォームプロパティウィンドウで定義できます。詳しくは、「フォームをオンラインで使 [用できるようにする」を参照してください](#making-a-form-available-online)

フォームのパブリッシュステータスがフォームのリストに表示されます。

![](assets/s_ncs_admin_survey_status.png)

### フォームのパブリッシュ {#publishing-a-form}

フォームの状態を変更するには、パブリッシュする必要があります。To do this, click the **[!UICONTROL Publication]** button above the list of Web forms and select the state in the drop-down box.

![](assets/webapp_publish_webform.png)

### フォームをオンラインで利用できるようにする {#making-a-form-available-online}

ユーザーがアクセスできるようにするためには、フォームは、本番で開始される必要があります。つまり、有効期間内にある必要があります。The validity dates are entered via the **[!UICONTROL Properties]** link of the form.

* Use the fields in the **[!UICONTROL Project]** section to enter start and end dates for the form.

   ![](assets/webapp_availability_date.png)

* リンクをク **[!UICONTROL Personalize the message displayed if the form is closed...]** リックして、無効な状態でユーザーがフォームにアクセスしようとした場合に表示されるエラーメッセージを定義します。

   See [Accessibility of the form](../../web/using/defining-web-forms-properties.md#accessibility-of-the-form).

### E メールによるフォームの配信 {#delivering-a-form-via-email}

When you deliver an invitation via email, you can use the **[!UICONTROL Adobe Campaign Encryption]** option for data reconciliation. これをおこなうには、配信ウィザードに移動して、次のパラメーターを追加することで、リンクをフォームに適応させます。

```
<a href="https://server/webApp/APP264?&id=<%=escapeUrl(recipient.cryptedId) %>">
```

この場合、データストレージの紐付けキーは、受信者の暗号化された識別子である必要があります。詳しくは、「フォームデータのプリロ [ード」を参照してください](#pre-loading-the-form-data)。

In this case, you need to check the **[!UICONTROL Update the preloaded record]** option in the record box. 詳しくは、「Webフォームの回答の保存」 [を参照してください](../../web/using/web-forms-answers.md#saving-web-forms-answers)。

![](assets/s_ncs_admin_survey_save_box_option.png)

### 応答をログに記録 {#log-responses}

回答のトラッキングを専用のタブで有効化すると、Web フォームの影響を監視することができます。To do this, click the **[!UICONTROL Advanced parameters...]** link in the form properties window and select the **[!UICONTROL Log responses]** option.

![](assets/s_ncs_admin_survey_trace.png)

The **[!UICONTROL Responses]** tab appears to let you view the identity of respondents.

![](assets/s_ncs_admin_survey_trace_tab.png)

Select a recipient and click the **[!UICONTROL Detail...]** button to view the responses provided.

![](assets/s_ncs_admin_survey_trace_edit.png)

例えば、リマインダーの送信時に非回答者のみをターゲットにしたり、回答者のみに特別なコミュニケーションを提供したりするために、クエリで提供された回答ログを処理できます。

>[!NOTE]
>
>提供された回答を完全にトラッキングし、回答をエクスポートして、専用のレポートを表示または作成するには、オプションの&#x200B;**調査**&#x200B;モジュールを使用します。詳しくは、[この節](../../web/using/about-surveys.md)を参照してください。

