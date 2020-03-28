---
title: 購読の管理
seo-title: 購読の管理
description: 購読の管理
seo-description: null
page-status-flag: never-activated
uuid: a2c526fa-3080-4dd5-9628-f0e7040f93cd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: subscriptions-and-referrals
discoiquuid: 9a61fe74-f779-4f23-be25-3d9a8e95704a
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# 購読の管理{#managing-subscriptions}

## 情報サービスについて {#about-information-services}

情報サービスは、次のもので構成されます。

* 登録および購読（オプトイン）
* 登録解除、自発的購読解除（オプトアウト）または自動購読解除（試用オファーなどの期間限定サービス）
* 購読および購読解除の確認の仕組み（確認を使用する単純な仕組みやダブルオプトインなど）
* 購読者履歴のトラッキング

標準機能として、これらのサービスには、購読者トラッキング、ロイヤリティレベル、購読解除のトレンドなど、固有の統計レポートが含まれます。

E メールの場合、必須の購読解除リンクが自動的に生成されて、オプトイン／オプトアウトプロセス全体が完全に自動化され、履歴をトラッキングすることで、実施基準に対する完全遵守を保証できます。

次の 3 つのサービス購読／購読解除モードがあります。

1. 手動
1. インポート（購読のみ）
1. Web フォーム

>[!NOTE]
>
>二重のオプトインを備えた購読フォームを作成する例については、[この節](../../web/using/use-cases--web-forms.md#create-a-subscription--form-with-double-opt-in)を参照してください。

## 情報サービスの作成 {#creating-an-information-service}

関連付けられた確認メッセージまたは購読者への自動配信を使用して、情報サービスを作成し、購読を管理できます。

情報サービスマップにアクセスするには、**[!UICONTROL プロファイルとターゲット]**&#x200B;ウィンドウに移動して、「**[!UICONTROL サービスと購読]**」リンクをクリックします。

![](assets/s_ncs_user_services_new.png)

既存のサービスを編集するには、サービス名をクリックします。サービスを作成するには、リストの上にある「**[!UICONTROL 作成]**」ボタンをクリックします。

![](assets/s_ncs_user_services_add.png)

* 「**[!UICONTROL ラベル]**」フィールドにサービスの名前を入力し、配信チャネル（E メール、モバイル、Facebook、Twitter またはモバイルアプリケーション）を選択します。

   >[!NOTE]
   >
   >Facebook と Twitter の購読については、[この節](../../social/using/about-social-marketing.md)で説明しています。モバイルアプリケーションの購読について詳しくは、[モバイルアプリチャネルについて](../../delivery/using/about-mobile-app-channel.md)を参照してください。

* E メールタイプのサービスの場合は、「**配信モード**」を選択します。選択できるモードは、「**[!UICONTROL ニュースレター]**」または「**[!UICONTROL バイラル]**」です。
* 購読または購読解除の&#x200B;**確認メッセージ**&#x200B;を送信できます。そのためには、対応する配信の作成に使用する配信テンプレートを「**[!UICONTROL 購読]**」フィールドおよび「**[!UICONTROL 購読解除]**」フィールドから選択します。このテンプレートは、定義済みのターゲットではなく、「**[!UICONTROL 購読]**」タイプのターゲットマッピングを使用して設定されている必要があります。[E メールチャネルについて](../../delivery/using/about-email-channel.md)の節を参照してください。
* デフォルトでは、購読は無制限です。「**[!UICONTROL 無制限]**」オプションを選択解除して、サービスの有効期間を定義できます。期間は日数（「**[!UICONTROL 日]**」）または月数（「**[!UICONTROL 月]**」）で指定できます。

サービスを保存すると、サービスと購読リストに追加されます。編集するにはサービス名をクリックします。複数のタブが表示されます。「**[!UICONTROL 購読]**」タブには、情報サービスの購読者のリスト（「**[!UICONTROL アクティブな購読]**」タブ）または購読／購読解除履歴（「**[!UICONTROL 履歴]**」タブ）を表示できます。また、このタブから購読者を追加および削除できます。[購読者の追加と削除](#adding-and-deleting-subscribers)を参照してください。

![](assets/s_ncs_user_services_subscriptions.png)

「**[!UICONTROL 詳細...]**」ボタンを使用して、選択した受信者の購読プロパティを表示できます。

受信者の購読プロパティは変更できます。

![](assets/s_ncs_user_services_modify.png)

ダッシュボードで「**[!UICONTROL レポート]**」タブをクリックして、購読レベルの変更、合計購読者数などの購読をトラッキングします。レポートをアーカイブして、このタブに履歴を表示できます。

## 購読者の追加と削除 {#adding-and-deleting-subscribers}

購読者を追加するには、情報サービスの「**[!UICONTROL 購読]**」タブから、「**[!UICONTROL 追加]**」をクリックします。購読者のリストを右クリックして、「**[!UICONTROL 追加]**」を選択することもできます。購読するプロファイルを保存するフォルダーを選択し、購読するプロファイルを選択し、「**[!UICONTROL OK]**」をクリックして確定します。

購読者を削除するには、購読者を選択して「**[!UICONTROL 削除]**」をクリックします。購読者のリストを右クリックして、「**[!UICONTROL 削除]**」を選択することもできます。

どちらの場合も、購読解除用の配信テンプレートがサービスに添付されていれば、該当するユーザーに確認メッセージを送信できます（[情報サービスの作成](#creating-an-information-service)を参照）。確認メッセージで、この配信を確定することも、しないこともできます。

![](assets/s_ncs_user_services_update.png)

[購読と購読解除の仕組み](#subscription-and-unsubscription-mechanisms)を参照してください。

## サービスの購読者への配信 {#delivering-to-the-subscribers-of-a-service}

情報サービスの購読者に配信するために、次の例のように、関連する情報サービスの購読者をターゲットにできます。

![](assets/s_ncs_user_wizard_target_is_a_service01.png)

>[!CAUTION]
>
>ターゲットマッピングは「**[!UICONTROL 購読]**」にする必要があります。

「**[!UICONTROL 情報サービスの購読者]**」を選択し、「**[!UICONTROL 次へ]**」をクリックします。

![](assets/s_ncs_user_wizard_target_is_a_service02.png)

ターゲットとする情報サービスを選択し、「**[!UICONTROL 完了]**」をクリックします。

![](assets/s_ncs_user_wizard_target_is_a_service03.png)

「**[!UICONTROL プレビュー]**」タブに、選択した情報サービスの購読者のリストが表示されます。

## 購読と購読解除の仕組み {#subscription-and-unsubscription-mechanisms}

購読および購読解除の仕組みを設定して、プロセスと購読者管理を自動化できます。

>[!NOTE]
>
>新しい購読者に確認メッセージを送信できます。\
>このメッセージの内容は、情報サービスの設定で、「**[!UICONTROL 購読]**」フィールドまたは「**[!UICONTROL 購読解除]**」フィールドから定義できます。
>
>確認メッセージは、このフィールドで指定した配信テンプレートから作成されます。このターゲットマッピングは「**[!UICONTROL 購読]**」にする必要があります。

![](assets/s_ncs_user_subscribe_confirmation.png)

### 受信者のサービスへの購読登録 {#subscribing-a-recipient-to-a-service}

次の方法で、受信者を情報サービスに登録できます。

* サービスを手動で追加するには、受信者のプロファイルの「**[!UICONTROL 購読]**」タブから「**[!UICONTROL 追加]**」をクリックし、該当する情報サービスを選択します。

   詳しくは、[この節](../../platform/using/editing-a-profile.md)のプロファイル編集に関する部分を参照してください。

* 一連の受信者をこのサービスに自動的に購読登録します。受信者のリストは、フィルタリング操作、グループ、フォルダー、インポートまたはマウスを使用した直接選択から取得できます。この受信者を購読登録するには、プロファイルを選択して右クリックします。**[!UICONTROL アクション／サービスの購読選択]**&#x200B;を選択し、該当するサービスを選択して、操作を開始します。
* 受信者をインポートして、情報サービスに自動的に購読登録します。そのためには、インポートウィザードの最後の手順で該当するサービスを選択します。

   詳しくは、[この節](../../platform/using/importing-data.md#import-wizard)を参照してください。

* 受信者をサービスに購読登録できる Web フォームを使用します。

   詳しくは、[この節](../../web/using/about-web-applications.md)を参照してください。

* ターゲティングワークフローを作成し、「**[!UICONTROL 購読サービス]**」ボックスを使用します。

   ![](assets/s_ncs_user_subscribe_from_wf.png)

   ワークフローとその使用方法については、[この節](../../workflow/using/about-workflows.md)で説明しています。

### 受信者のサービスからの購読解除 {#unsubscribing-a-recipient-from-a-service}

#### 手動購読解除 {#manual-unsubscribing}

法令により、E メール配信には購読解除リンクを含める必要があります。受信者は、このリンクをクリックして自分のプロファイルを更新し、今後の配信のターゲットから除外させることができます。

デフォルトの購読解除リンクは、配信ウィザードに表示されるコンテンツエディターのツールバーにある最後のボタンから挿入されます（[パーソナライゼーションについて](../../delivery/using/about-personalization.md)を参照）。受信者がこのリンクをクリックすると、プロファイルがブラックリストに登録されます（オプトアウト）。つまり、この受信者は、あらゆる配信アクションのターゲットにされなくなります。

ただし、受信者は、すべてのサービスを購読解除することなく、1 つのサービスの購読解除を選択できます。この選択を可能にするには、Web フォームを使用するか（[この節](../../web/using/adding-fields-to-a-web-form.md#subscription-checkboxes)を参照）、パーソナライズされた購読解除リンクを挿入します（[パーソナライゼーションブロック](../../delivery/using/personalization-blocks.md)を参照）。

受信者プロファイルから手動で受信者を購読解除することもできます。そのためには、該当する受信者の「**[!UICONTROL 購読]**」タブをクリックし、該当する情報サービスを選択し、「**[!UICONTROL 削除]**」をクリックします。

また、該当する情報サービスから、1 人以上の受信者を購読解除できます。そのためには、その情報サービスの「**[!UICONTROL 購読]**」タブをクリックし、該当する受信者を選択し、「**[!UICONTROL 削除]**」をクリックします。

#### 自動購読解除 {#automatic-unsubscription}

情報サービスの期間を限定することができます。有効期間が期限切れになると、受信者は自動的に購読解除されます。この期間は、サービスプロパティの「**[!UICONTROL 編集]**」タブで指定します。期間は日数で表します。

![](assets/s_ncs_user_services_delay.png)

母集団の購読解除ワークフローを設定することもできます。そのためには、購読ワークフローと同じ手順に従いますが、「**[!UICONTROL 購読解除]**」オプションを選択します。[受信者のサービスへの購読登録](#subscribing-a-recipient-to-a-service)を参照してください。

### 購読者トラッキング {#subscriber-tracking}

ダッシュボードの「**[!UICONTROL レポート]**」リンクを使用して、情報サービスの購読の推移をトラッキングできます。

![](assets/s_ncs_user_services_report.png)
