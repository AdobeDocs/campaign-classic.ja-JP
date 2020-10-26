---
title: Facebook へのパブリッシュ
seo-title: Facebook へのパブリッシュ
description: Facebook へのパブリッシュ
seo-description: null
page-status-flag: never-activated
uuid: f15170fa-0e7d-4913-81d6-0072c1ece482
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: social
content-type: reference
topic-tags: publishing-on-facebook-twitter
discoiquuid: 335cf2de-1874-4e48-9538-f0937641cf96
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '1256'
ht-degree: 100%

---


# Facebook へのパブリッシュ{#publishing-on-facebook}

設定が完了すると、ソーシャルマーケティングで Facebook ページのウォールにパブリケーションを投稿できます。

## 制限事項 {#limitations}

Facebook には次の制限があります。

* メッセージの長さは 1 000 文字以下にする必要があります。
* HTML はサポートされていません。

## 配信の作成 {#creating-the-delivery}

「**[!UICONTROL ブランドページにパブリッシュ]**」配信テンプレートを使用して、新しい配信を作成します。

![](assets/social_facebook_delivery_001.png)

## メインターゲットの選択 {#selecting-the-main-target}

パブリケーションを投稿するページを選択する必要があります。

1. 「**[!UICONTROL 宛先]**」リンクをクリックします。

   ![](assets/social_facebook_delivery_010.png)

1. 「**[!UICONTROL 追加]**」ボタンをクリックします。

   ![](assets/social_facebook_delivery_011.png)

1. **[!UICONTROL Facebook ページ]**&#x200B;を選択します。

   ![](assets/social_facebook_delivery_012.png)

1. 「**[!UICONTROL フォルダー]**」フィールドで、Facebook ページを含むサービスフォルダーを選択します。デフォルトでは、ページは **[!UICONTROL Facebook]** サービスフォルダーのルートに保存されます。次に、投稿先の Facebook ページを選択します。

   ![](assets/social_facebook_delivery_013.png)

## 配達確認のターゲットの選択 {#selecting-the-proof-target}

「**[!UICONTROL 配達確認のターゲット]**」タブでは、配信を送信する前に、テスト目的で使用する Facebook ページを定義できます。この目的で利用する専用の非公開 Facebook ページを作成することをお勧めします。非公開 Facebook ページの作成について詳しくは、[テスト用 Facebook ページの作成](../../social/using/publishing-on-facebook-walls.md#creating-a-test-facebook-page)を参照してください。配達確認のターゲットを選択するには、メインターゲットと同じ手順を適用します。[メインターゲットの選択](#selecting-the-main-target)を参照してください。

![](assets/social_facebook_delivery_004.png)

>[!NOTE]
>
>すべての配信に同じ Facebook テストページを使用する場合、「**[!UICONTROL ブランドページにパブリッシュ]**」配信テンプレートに配達確認のターゲットを保存できます。このテンプレートには、**[!UICONTROL リソース／テンプレート／配信テンプレート]**&#x200B;ノードからアクセスできます。これにより、新規の各配信で、配達確認のターゲットがデフォルトで入力されるようになります。

## オーディエンスの定義 {#defining-the-audience}

ローカルセグメントを利用してパブリケーションが表示される一般ユーザーのタイプを絞り込みたい場合、各セグメント用にそれぞれ 1 つの Facebook ページ（例：Adobe Campaign Paris、Adobe Campaign London など）を作成することをお勧めします。

ただし、Facebook で使用されるオーディエンスフィルターを使用することもできます。**[!UICONTROL ターゲットを選択]**&#x200B;ウィンドウの「**[!UICONTROL オーディエンス]**」タブでは、次の 4 つのフィルターを提供します。

* **[!UICONTROL 国]**
* **[!UICONTROL 地域]**
* **[!UICONTROL 市区町村]**
* **[!UICONTROL 言語]**

>[!IMPORTANT]
>
>このオプションを使用する際は注意してください。配信レポートでは、**[!UICONTROL ファン数]**&#x200B;の指標はこうした Facebook フィルターを考慮しません。
>
>Facebook は、オーディエンスフィルターのリストと値を変更する可能性があります。

## メッセージコンテンツの定義 {#defining-message-content}

**[!UICONTROL コンテンツタイプ]**&#x200B;のドロップダウンメニューを利用してパブリッシュの種類を選択します。

![](assets/social_facebook_delivery_006.png)

次のようなタイプの配信が利用できます。

* **[!UICONTROL ステータス]**
* **[!UICONTROL リンク付きステータス]**
* **[!UICONTROL YouTube リンク付きステータス]**
* **[!UICONTROL フォトアルバム]**

### ステータスのパブリッシュ {#publishing-a-status}

ステータスタイプの配信には、次の例のようにテキストのみを含めることができます。

![](assets/social_create_facebook_wall_post_004.png)

入力ゾーンにパブリッシュステータスを入力します。

![](assets/social_facebook_delivery_015.png)

### リンク付きステータスのパブリッシュ {#publishing-a-status-with-a-link}

リンク付きステータスタイプの配信には、テキスト、画像、およびリンクを含めることができます。以下の節では、配信編集画面のフィールドと Facebook 上の最終的な投稿との相関について説明します。

![](assets/social_facebook_delivery_007.png)

次の各フィールドを入力します。

>[!IMPORTANT]
>
>すべての URL は、**「http://」**&#x200B;または&#x200B;**「https://」**&#x200B;で始まる必要があります。

1. 「**[!UICONTROL ステータス]**」フィールドに、ページ名の下に表示するテキストを入力します。
1. 「**[!UICONTROL 名前]**」フィールドに、パブリケーションのタイトルを入力します。
1. 「**[!UICONTROL リンク]**」フィールドに、パブリケーションが指す URL を入力します。

   >[!NOTE]
   >
   >「**[!UICONTROL リンク]**」フィールドに Facebook アプリケーションの URL を追加してプロモーションする場合は、スマートフォンのディスプレイ条件に適合させることをお勧めします。
   >
   >1. Facebook アプリケーションを選択し（[https://developers.facebook.com/apps](https://developers.facebook.com/apps)）、**[!UICONTROL 設定／ベーシック]**&#x200B;タブを選択します。
   >1. 「**[!UICONTROL 名前空間]**」フィールドに入力します。
   >1. 「**[!UICONTROL モバイルサイトの URL]**」フィールドに入力します。ユーザーがスマートフォンでパブリケーションのリンクをクリックすると、Facebook はこのフィールドに定義された URL にユーザーを自動的にリダイレクトします。
   >1. Web アプリケーションを作成する際には、使用するデバイス（スマートフォンまたは PC ）によって Facebook の表示がパーソナライズされるようにします。
   >1. Adobe Campaign コンソールを使用してパブリケーションの「**[!UICONTROL リンク]**」フィールドに移動し、「**[!UICONTROL キャンバスページ]**」フィールドの URL を入力します。


1. 「**[!UICONTROL 画像]**」フィールドに、パブリケーションの左側に表示する画像の URL を入力します。

   >[!IMPORTANT]
   >
   >Facebook に画像をアップロードするには、公開インターネットサイトで画像をホストする必要があります。

1. 「**[!UICONTROL キャプション]**」フィールドに、パブリケーションの末尾に表示するテキストを入力します。
1. 「**[!UICONTROL 説明]**」フィールドに移動し、タイトルの下に表示するテキストを入力します。

![](assets/social_facebook_delivery_005.png)

### YouTube リンク付きステータスのパブリッシュ {#publishing-a-status-with-a-youtube-link}

このタイプのコンテンツを使用すると、YouTube 動画へのリンクを投稿できます。通常のリンク付きステータスと同様に、ステータス、名前、キャプション、説明および追加のリンクを定義できます。画像は Facebook が自動的に追加します。配信編集画面のフィールドと Facebook 上の最終的な投稿との相関を以下に示します。

![](assets/social_facebook_delivery_youtube_1.png)

次の各フィールドを入力します。

>[!CAUTION]
>
>すべての URL は、**「http://」**&#x200B;または&#x200B;**「https://」**&#x200B;で始まる必要があります。

1. 「**[!UICONTROL ステータス]**」フィールドに、ページ名の下に表示するテキストを入力します。
1. 「**[!UICONTROL 名前]**」フィールドに、パブリケーションのタイトルを入力します。
1. 「**[!UICONTROL ビデオコード]**」フィールドに、YouTube 動画のコードを入力します。例えば、「https://www.youtube.com/watch?v=abc123456」というリンクの場合、ビデオコードは「abc123456」です。
1. 「**[!UICONTROL キャプション]**」フィールドに、パブリケーションの末尾に表示するテキストを入力します。
1. 「**[!UICONTROL 説明]**」フィールドに移動し、タイトルの下に表示するテキストを入力します。

![](assets/social_facebook_delivery_youtube.png)

### フォトアルバムのパブリッシュ {#publishing-a-photo-album}

このタイプのコンテンツを使用すると、フォトアルバムをパブリッシュできます。アルバムの名前と説明、さらに各写真のキャプションを追加できます。配信編集画面のフィールドと Facebook 上の最終的な投稿との相関を以下に示します。

![](assets/social_facebook_delivery_photos_1.png)

次の各フィールドを入力します。

1. まず「**[!UICONTROL アルバム名]**」を入力します。
1. 次に、写真の上に表示する「**[!UICONTROL 説明]**」を入力します。
1. 写真を追加するには、「**[!UICONTROL 追加]**」ボタンをクリックし、写真を選択して「**[!UICONTROL 開く]**」をクリックします。
1. キャプションは各写真に追加できます。

![](assets/social_facebook_delivery_photos.png)

## プレビュー {#previewing}

「**[!UICONTROL プレビュー]**」タブでは、パブリケーションのレンダリングを表示できます。

1. 「**[!UICONTROL プレビュー]**」タブをクリックします。
1. 「**[!UICONTROL パーソナライゼーションをテスト]**」ドロップダウンメニューをクリックし、「**[!UICONTROL サービス]**」を選択します。
1. 「**[!UICONTROL フォルダー]**」フィールドで、Facebook ページを含むサービスフォルダーを選択します。デフォルトでは、ページは **[!UICONTROL Facebook]** サービスフォルダーのルートに保存されます。
1. プレビューをテストする Facebook ページを選択します。

![](assets/social_facebook_delivery_008.png)

>[!NOTE]
>
>プレビューは、Facebook 上の最終的な投稿とは多少異なる場合があります。最終的な配信の前に、配達確認を送信してパブリケーションの正確なレンダリングを確認することを強くお勧めします。[配達確認の送信](#sending-the-proof)を参照してください。

## トラッキングの設定 {#configuring-tracking}

トラッキングは、配信レポート、さらに配信とサービスの&#x200B;**[!UICONTROL 編集／「追跡」]**&#x200B;タブで表示できます。

配信に含まれる URL のクリック数は、Adobe Campaign が測定します。「**[!UICONTROL いいね！]**」ボタンのクリック数、コメント数およびファン数は、Facebook が測定します。

トラッキング設定は、E メール配信の場合と同じです。詳しくは、[この節](../../delivery/using/monitoring-a-delivery.md)を参照してください。

>[!NOTE]
>
>「**[!UICONTROL ブランドページにパブリッシュ]**」配信テンプレートでは、トラッキングがデフォルトで有効になっています。

## 配達確認の送信 {#sending-the-proof}

最終的な配信の前に、パブリケーションの配達確認を送信してテスト用の非公開 Facebook ページでパブリケーションの正確なレンダリングを確認することを強くお勧めします。テスト用の非公開 Facebook ページの作成について詳しくは、[テスト用 Facebook ページの作成](../../social/using/publishing-on-facebook-walls.md#creating-a-test-facebook-page)を参照してください。配達確認のターゲットを選択する手順について詳しくは、[配達確認のターゲットの選択](#selecting-the-proof-target)を参照してください。

配達確認の配信は、E メールの配信と同じです。[この節](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)を参照してください。

## メッセージの送信 {#sending-the-message}

1. コンテンツが承認されたら、「**[!UICONTROL 送信]**」ボタンをクリックします。
1. 「**[!UICONTROL 可能な限り早く配信]**」を選択し、「**[!UICONTROL 分析]**」ボタンをクリックします。

   >[!NOTE]
   >
   >「**[!UICONTROL 配信を延期]**」オプションを使用すると、後日まで配信を延期できます。

   ![](assets/social_facebook_delivery_009.png)

1. 分析が完了したら、結果を確認します。
1. 「**[!UICONTROL 配信を確定]**」をクリックし、「**[!UICONTROL はい]**」をクリックします。

   ![](assets/social_facebook_delivery_016.png)

