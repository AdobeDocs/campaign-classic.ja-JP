---
title: Twitter へのパブリッシュ
seo-title: Twitter へのパブリッシュ
description: Twitter へのパブリッシュ
seo-description: null
page-status-flag: never-activated
uuid: 405bce50-a63c-4bd3-8f03-c71809bb1cfd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: publishing-on-facebook-twitter
discoiquuid: 2dc278ce-477c-493d-8abb-8bbdf2e988a5
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '1029'
ht-degree: 100%

---


# Twitter へのパブリッシュ{#publishing-on-twitter}

## Twitter アカウントへのパブリッシュ {#publishing-on-your-twitter-accounts}

設定が完了すると、ソーシャルマーケティングで Twitter アカウントにツイートを送信できます。

### 制限事項 {#limitations}

Twitter には次の制限があります。

* メッセージの長さは 140 文字以下にする必要があります。
* HTML はサポートされていません。

### 配信の作成 {#creating-the-delivery}

「**[!UICONTROL ツイート（Twitter）]**」配信テンプレートに基づいて新しい配信を作成します。

![](assets/social_twitter_delivery_001.png)

### メインターゲットの選択 {#selecting-the-main-target}

ツイートの送信先アカウントを選択します。

1. 「**[!UICONTROL 宛先]**」リンクをクリックします。

   ![](assets/social_twitter_delivery_002.png)

1. 「**[!UICONTROL 追加]**」ボタンをクリックします。

   ![](assets/social_twitter_delivery_006.png)

1. 「**[!UICONTROL Twitter アカウント]**」を選択します。

   ![](assets/social_twitter_delivery_007.png)

1. 「**[!UICONTROL フォルダー]**」フィールドで、Twitter アカウントを含むサービスフォルダーを選択します。次に、ツイートを送信する Twitter アカウントを選択します。

   ![](assets/social_twitter_delivery_011.png)

### 配達確認のターゲットの選択 {#selecting-the-target-of-the-proof}

「**[!UICONTROL 配達確認のターゲット]**」タブでは、最終的な配信の前に、テスト目的で使用する Twitter アカウントを定義できます。このため、配達確認の送信専用に使用する専用の非公開 Twitter アカウントを作成することをお勧めします。非公開 Twitter アカウントを作成する方法について詳しくは、[Twitter でのテストアカウントの作成](../../social/using/configuring-publishing-on-twitter.md#creating-a-test-account-on-twitter)を参照してください。配達確認のターゲットを選択する手順は、メインターゲットを選択する手順と同じです。[Twitter でのテストアカウントの作成](../../social/using/configuring-publishing-on-twitter.md#creating-a-test-account-on-twitter)を参照してください。

![](assets/social_twitter_delivery_004.png)

>[!NOTE]
>
>すべての配信に同じ Twitter テストアカウントを使用する場合、「**[!UICONTROL ツイート]**」配信テンプレートに配達確認のターゲットを保存できます。このテンプレートには、**[!UICONTROL リソース／テンプレート／配信テンプレート]**&#x200B;ノードからアクセスできます。これにより、新規の各配信で、配達確認のターゲットがデフォルトで入力されるようになります。

### メッセージコンテンツの定義 {#defining-the-message-content}

「**[!UICONTROL コンテンツ]**」タブにツイートの内容を入力します。

![](assets/social_twitter_delivery_005.png)

### プレビューの表示 {#viewing-the-preview}

「**[!UICONTROL プレビュー]**」タブでは、ツイートのレンダリングを表示できます。

1. 「**[!UICONTROL プレビュー]**」タブをクリックします。
1. 「**[!UICONTROL パーソナライゼーションをテスト]**」ドロップダウンメニューをクリックし、「**[!UICONTROL サービス]**」を選択します。
1. 「**[!UICONTROL フォルダー]**」フィールドで、Twitter アカウントを含むサービスフォルダーを選択します。
1. プレビューをテストする Twitter アカウントを選択します。

![](assets/social_twitter_delivery_008.png)

>[!NOTE]
>
>プレビューは、最終的なツイートとは多少異なる場合があります。最終的な配信の前に、配達確認を送信してツイートの正確なレンダリングを確認することを強くお勧めします。[配達確認の送信](#sending-the-proof)を参照してください。

### トラッキングの設定 {#configuring-tracking}

トラッキングは、配信レポート、さらに配信とサービスの&#x200B;**[!UICONTROL 編集／「トラッキング」]**&#x200B;タブで表示できます。

トラッキング設定は、E メール配信の場合と同じです。詳しくは、[この節](../../delivery/using/monitoring-a-delivery.md)を参照してください。

>[!NOTE]
>
>「**[!UICONTROL ツイート]**」配信テンプレートでは、トラッキングがデフォルトで有効になっています。

>[!IMPORTANT]
>
>ツイートを分析するロボットと実際にクリックしているユーザーの違いを見分けることはできません。

### 配達確認の送信 {#sending-the-proof}

最終的な配信の前に、パブリケーションの配達確認を送信してテスト用の非公開 Twitter ページでパブリケーションの正確なレンダリングを確認することを強くお勧めします。非公開 Twitter アカウントの作成について詳しくは、[Twitter でのテストアカウントの作成](../../social/using/configuring-publishing-on-twitter.md#creating-a-test-account-on-twitter)を参照してください。配達確認のターゲットを選択する手順について詳しくは、[配達確認のターゲットの選択](#selecting-the-target-of-the-proof)を参照してください。

配達確認の配信は、E メールの配信と同じです。[この節](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)を参照してください。

### メッセージの送信 {#sending-the-message}

1. コンテンツが承認されたら、「**[!UICONTROL 送信]**」ボタンをクリックします。
1. 「**[!UICONTROL 可能な限り早く配信]**」を選択し、「**[!UICONTROL 分析]**」ボタンをクリックします。

   >[!NOTE]
   >
   >「**[!UICONTROL 配信を延期]**」オプションを使用すると、後日まで配信を延期できます。

   ![](assets/social_twitter_delivery_012.png)

1. 分析が完了したら、結果を確認します。
1. 「**[!UICONTROL 配信を確定]**」をクリックし、「**[!UICONTROL はい]**」をクリックします。

![](assets/social_facebook_delivery_016.png)

## 購読者へのダイレクトメッセージの送信 {#sending-direct-messages-to-subscribers}

### 動作の仕組み {#operating-principle}

「**[!UICONTROL Twitter アカウントを同期]**」ワークフロー（[Twitter アカウントの同期](../../social/using/configuring-publishing-on-twitter.md#synchronizing-twitter-accounts)を参照）は、Twitter 購読者のリストを取得して、ダイレクトメッセージを送信できるようにします。取得したフォロワーは、「訪問者」という特定のテーブルに格納されます。Twitter フォロワーのリストを表示するには、**[!UICONTROL プロファイルとターゲット／訪問者]**&#x200B;ノードに移動します。

![](assets/social_twitter_visitors_001.png)

>[!IMPORTANT]
>
>ワークフローが Twitter フォロワーのリストを取得するには、アカウントにリンクされたサービスの編集画面で「**[!UICONTROL Twitter アカウントを同期]**」ボックスをオンにする必要があります。詳しくは、[Adobe Campaign への書き込みアクセス権のデリゲート](../../social/using/configuring-publishing-on-twitter.md#delegating-write-access-to-adobe-campaign)を参照してください。

Adobe Campaign は、各フォロワーについて次の情報を取得します。

* **[!UICONTROL 生成元]**：ソーシャルネットワークの名前（この場合、**Twitter**）
* **[!UICONTROL 外部 ID]**：ユーザー識別子
* **[!UICONTROL ユーザー名]**：ユーザーのアカウント名
* **[!UICONTROL フルネーム]**：ユーザーの名前
* **[!UICONTROL 言語]**：ユーザーの言語
* **[!UICONTROL 友達の数]**：フォロワー数
* **[!UICONTROL タイムゾーン]**：ユーザーのタイムゾーン
* **[!UICONTROL 検証済み]**：ユーザーが検証済みの Twitter アカウントを持っているかを示すフィールド

### 制限事項 {#limitations-1}

Twitter には次の制限があります。

* メッセージの長さは 140 文字以下にする必要があります。
* HTML はサポートされていません。
* 1 日に 250 件を超えるダイレクトメッセージを送信することはできません。このしきい値を超えないようにするには、複数のウェーブで配信します。ウェーブでの配信は、E メール配信の場合と同じように設定します。詳しくは、[この節](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を参照してください。

### 配信の作成 {#creating-the-delivery-}

「**[!UICONTROL ツイート（ダイレクトメッセージ）]**」配信テンプレートに基づいて新しい配信を作成します。

![](assets/social_twitter_delivery_010.png)

### メインターゲットの選択 {#selecting-the-main-target-1}

ダイレクトメッセージを送信するフォロワーを選択します。

1. 「**[!UICONTROL 宛先]**」リンクをクリックします。

   ![](assets/social_twitter_delivery_016.png)

1. 「**[!UICONTROL 追加]**」ボタンをクリックします。

   ![](assets/social_twitter_delivery_006.png)

1. ターゲティングのタイプを選択します。

   ![](assets/social_twitter_delivery_017.png)

   * 「**[!UICONTROL Twitter 購読者]**」を選択し、アカウントのフォロワー全員にダイレクトメッセージを送信します。

      >[!IMPORTANT]
      >
      >1 日に 250 件を超えるメッセージを送信することはできません。Twitter アカウントに 250 人を超えるフォロワーがいる場合は、複数のウェーブで配信することを強くお勧めします。これには、E メール配信と同じ手順が必要です。[この節](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を参照してください。

   * 「**[!UICONTROL フィルター条件]**」を選択し、クエリを定義して結果を表示します。このオプションは、E メール配信の場合と同じです。詳しくは、[この節](../../platform/using/defining-filter-conditions.md)を参照してください。

      ![](assets/social_twitter_delivery_018.png)

### 配達確認のターゲットの選択 {#selecting-the-target-of-the-proof-1}

「**[!UICONTROL 配達確認のターゲット]**」タブでは、ダイレクトメッセージの配達確認を受信するフォロワーを選択できます。選択する手順は、メインターゲットの場合と同じです。[メインターゲットの選択](#selecting-the-main-target)を参照してください。

![](assets/social_twitter_delivery_020.png)

>[!NOTE]
>
>すべてのダイレクトメッセージの配達確認を同じ Twitter フォロワーに送信する場合、「**[!UICONTROL ツイート（ダイレクトメッセージ）]**」配信テンプレートに配達確認のターゲットを保存できます。このテンプレートには、**[!UICONTROL リソース／テンプレート／配信テンプレート]**&#x200B;ノードからアクセスできます。これにより、新規の各配信で、配達確認のターゲットがデフォルトで入力されるようになります。

### メッセージコンテンツの定義 {#defining-message-content-}

「**[!UICONTROL コンテンツ]**」タブにツイートの内容を入力します。

![](assets/social_twitter_delivery_015.png)

パーソナライゼーションフィールドは、E メール配信と同じ手順で使用可能です。例えば、メッセージの本文にフォロワーの名前を追加できます。コンテンツのパーソナライゼーションについて詳しくは、[この節](../../delivery/using/about-personalization.md)で説明しています。

![](assets/social_twitter_delivery_021.png)

残りの手順は、ツイートを Twitter アカウントに送信する場合と同じです。[Twitter アカウントへのパブリッシュ](#publishing-on-your-twitter-accounts)を参照してください。
